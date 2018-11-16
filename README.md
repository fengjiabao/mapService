## A JS data store and Component communication service

**Install**

1. **npm install mapservice**

**Basic description**

1. Js global access data store

2. Complete inter-component communication and data transfer

3. Smaller and more refined data layer than vuex, does not depend on any framework


**API**
 #### 1. DataStore
 **Js global access data store**
 ```javascript
/*
 * js 数据层
 * @author fengjiabao
 * @link:  https://github.com/fengjiabao/mapService
 * @version 1.0.3
 */
import mapService from 'mapservice' //   or   var  mapService = require("mapservice") 

// set data
mapService.DataStore.set('loginStatus' : {
    login: "true",
    cookie: "p00001"
} )

mapService.DataStore.set("userList" : [liming,liliy, wangfei])

mapService.DataStore.set("userNumber" : 15)

//get data
mapService.DataStore.get("loginStatus")

//update data
mapService.DataStore.set("loginStatus",{ //set all value
	login: "false",
	cookie: "p00002"
})

mapService.DataStore.setObjVal("loginStatus.login","false") //Set obj a key value

mapService.DataStore.setObjVal("loginStatus.cookie",["p0001","p0003"]) //Set obj a key value

// delete data
mapService.DataStore.delete("loginStatus")

//Get whether there is a key
mapService.DataStore.hasKey("loginStatus")

// clear mapService dataStore
mapService.DataStore.clear()

//get store values
mapService.DataStore.values()

//get store keys
mapService.DataStore.keys()

//get store size
mapService.DataStore.size()
```
 #### 2.  dataService
**Complete inter-component communication and data transfer**
 ##### eg1:
 ```javascript
 //component 1,before mounted
 mapService.on("goLogin",function(data){
 	data.user && data.pwd && goLogin() 
 })
 
 //component 2, trigger event
 mapService.trigger("goLogin",{
 	user: "nike",
	 pwd: "123"
 })
 
 ```
  ##### eg2:
 ```javascript
 //Registered in main.js
 mapService.on("goLogin",function(data){
 	data.user && data.pwd && goLogin() 
 })
 
 //async event
 axios.post("//www.npmjs.com",params,function(data){
 	mapService.trigger("goLogin",data)
 })
 
 ```
 
   ##### eg3: Multiple subscribers
 ```javascript
 //component 1,before mounted
 mapService.on("goLogin",function(data){
 	data.user && data.pwd && goLogin() 
 })
 
  //component 3,before mounted
 mapService.on("goLogin",function(data){
 	data.user && data.pwd && goLogin() 
 })
 
 //component 2, trigger event
 mapService.trigger("goLogin",{
 	user: "nike",
	 pwd: "123"
 })
 
 ```
 ##### Execute once:
 ```javascript
 //Registered in main.js
 mapService.once("goLogin",function(data){
 	data.user && data.pwd && goLogin() 
 })
 
 //async event
 axios.post("//www.npmjs.com",params,function(data){
 	mapService.trigger("goLogin",data)
 })
 ```
 
 ##### off event:
	
 ```javascript
 mapService.off("goLogin")
 
 ```
 ### If you have any interest or question, welcome to fork https://github.com/fengjiabao/mapService