---
title: SIMULATION: Running multiple tasks on limited number of resources
description: 
created: 2017-12-08
---

```javascript 
const AVAILABLE_DEVICES = 10;
const TASK_EXECUTION_TIME = 1000;

// creating 10 devices
const devices = [];
for (let i = 0; i < AVAILABLE_DEVICES; i++) {
    devices.push({
        id: i,
        status: true // true = available
    })
}


const pendingRequests = []
// gives a device in future
async function getDevice() {
    let _resolve, _reject;
    let promise = new Promise((resolve, reject) => { _reject = reject; _resolve = resolve; });
    let availableDevices = devices.filter(ele => ele.status)
    if(availableDevices && availableDevices.length > 0){
        availableDevices[0].status = false;
        _resolve(availableDevices[0]);
    }else{
        pendingRequests.push(_resolve);
    }
    return promise;
}

function processPendingRequests(){
    if(pendingRequests.length > 0){
        let availableDevices = devices.filter(ele => ele.status)
        if(availableDevices && availableDevices.length > 0){
            availableDevices[0].status = false;
            pendingRequests[0](availableDevices[0])
            pendingRequests.shift();
        }else{
            console.log('This should not happen');
        }
    }
}

function releaseDevice(id){
    devices.filter(ele => ele.id === id)[0].status = true;
    processPendingRequests();
}

//function that simulate real device execution, every execution takes 1 sec
async function execute(task) {
    let _resolve, _reject;
    let promise = new Promise((resolve, reject) => { _reject = reject; _resolve = resolve; });
    let device = await getDevice();
    console.log(`task:${task.id} got device. device id: ${device.id}`)
    // execute task on device
    setTimeout(() => {
        _resolve(true);
        console.log(`task:${task.id} release device`)
        releaseDevice(device.id);
        console.log(`task:${task.id} completed`)
    }, TASK_EXECUTION_TIME);
    return promise;
}

// Creating 100 sample tasks
let tasks = [];
for (let id = 0; id < 100; id++) {
    tasks.push({ id });
}

function executeTasks(tasks) {
    let promises = [];
    for(let task of tasks){
        console.log(`task:${task.id} started`);
        promises.push(execute(task));
    }
    Promise.all(promises).then((vs) => {
        console.log('Finished all tasks');
    });
}

executeTasks(tasks);

(function wait () { if (true) setTimeout(wait, 1000); })();
```


### Output: 

```
MacBook-Pro$ node index.js
10 devices created
task:0 started
task:1 started
task:2 started
task:3 started
task:4 started
task:5 started
task:6 started
task:7 started
task:8 started
task:9 started
task:10 started
task:11 started
task:12 started
task:13 started
task:14 started
task:15 started
task:16 started
task:17 started
task:18 started
task:19 started
task:20 started
task:21 started
task:22 started
task:23 started
task:24 started
task:25 started
task:26 started
task:27 started
task:28 started
task:29 started
task:30 started
task:31 started
task:32 started
task:33 started
task:34 started
task:35 started
task:36 started
task:37 started
task:38 started
task:39 started
task:40 started
task:41 started
task:42 started
task:43 started
task:44 started
task:45 started
task:46 started
task:47 started
task:48 started
task:49 started
task:50 started
task:51 started
task:52 started
task:53 started
task:54 started
task:55 started
task:56 started
task:57 started
task:58 started
task:59 started
task:60 started
task:61 started
task:62 started
task:63 started
task:64 started
task:65 started
task:66 started
task:67 started
task:68 started
task:69 started
task:70 started
task:71 started
task:72 started
task:73 started
task:74 started
task:75 started
task:76 started
task:77 started
task:78 started
task:79 started
task:80 started
task:81 started
task:82 started
task:83 started
task:84 started
task:85 started
task:86 started
task:87 started
task:88 started
task:89 started
task:90 started
task:91 started
task:92 started
task:93 started
task:94 started
task:95 started
task:96 started
task:97 started
task:98 started
task:99 started
task:0 got device. device id: 0
task:1 got device. device id: 1
task:2 got device. device id: 2
task:3 got device. device id: 3
task:4 got device. device id: 4
task:5 got device. device id: 5
task:6 got device. device id: 6
task:7 got device. device id: 7
task:8 got device. device id: 8
task:9 got device. device id: 9
task:0 release device
task:0 completed
task:1 release device
task:1 completed
task:2 release device
task:2 completed
task:3 release device
task:3 completed
task:4 release device
task:4 completed
task:5 release device
task:5 completed
task:6 release device
task:6 completed
task:7 release device
task:7 completed
task:8 release device
task:8 completed
task:9 release device
task:9 completed
task:10 got device. device id: 0
task:11 got device. device id: 1
task:12 got device. device id: 2
task:13 got device. device id: 3
task:14 got device. device id: 4
task:15 got device. device id: 5
task:16 got device. device id: 6
task:17 got device. device id: 7
task:18 got device. device id: 8
task:19 got device. device id: 9
task:10 release device
task:10 completed
task:11 release device
task:11 completed
task:12 release device
task:12 completed
task:13 release device
task:13 completed
task:14 release device
task:14 completed
task:15 release device
task:15 completed
task:16 release device
task:16 completed
task:17 release device
task:17 completed
task:18 release device
task:18 completed
task:19 release device
task:19 completed
task:20 got device. device id: 0
task:21 got device. device id: 1
task:22 got device. device id: 2
task:23 got device. device id: 3
task:24 got device. device id: 4
task:25 got device. device id: 5
task:26 got device. device id: 6
task:27 got device. device id: 7
task:28 got device. device id: 8
task:29 got device. device id: 9
task:20 release device
task:20 completed
task:21 release device
task:21 completed
task:22 release device
task:22 completed
task:23 release device
task:23 completed
task:24 release device
task:24 completed
task:25 release device
task:25 completed
task:26 release device
task:26 completed
task:27 release device
task:27 completed
task:28 release device
task:28 completed
task:29 release device
task:29 completed
task:30 got device. device id: 0
task:31 got device. device id: 1
task:32 got device. device id: 2
task:33 got device. device id: 3
task:34 got device. device id: 4
task:35 got device. device id: 5
task:36 got device. device id: 6
task:37 got device. device id: 7
task:38 got device. device id: 8
task:39 got device. device id: 9
task:30 release device
task:30 completed
task:31 release device
task:31 completed
task:32 release device
task:32 completed
task:33 release device
task:33 completed
task:34 release device
task:34 completed
task:35 release device
task:35 completed
task:36 release device
task:36 completed
task:37 release device
task:37 completed
task:38 release device
task:38 completed
task:39 release device
task:39 completed
task:40 got device. device id: 0
task:41 got device. device id: 1
task:42 got device. device id: 2
task:43 got device. device id: 3
task:44 got device. device id: 4
task:45 got device. device id: 5
task:46 got device. device id: 6
task:47 got device. device id: 7
task:48 got device. device id: 8
task:49 got device. device id: 9
task:40 release device
task:40 completed
task:41 release device
task:41 completed
task:42 release device
task:42 completed
task:43 release device
task:43 completed
task:44 release device
task:44 completed
task:45 release device
task:45 completed
task:46 release device
task:46 completed
task:47 release device
task:47 completed
task:48 release device
task:48 completed
task:49 release device
task:49 completed
task:50 got device. device id: 0
task:51 got device. device id: 1
task:52 got device. device id: 2
task:53 got device. device id: 3
task:54 got device. device id: 4
task:55 got device. device id: 5
task:56 got device. device id: 6
task:57 got device. device id: 7
task:58 got device. device id: 8
task:59 got device. device id: 9
task:50 release device
task:50 completed
task:51 release device
task:51 completed
task:52 release device
task:52 completed
task:53 release device
task:53 completed
task:54 release device
task:54 completed
task:55 release device
task:55 completed
task:56 release device
task:56 completed
task:57 release device
task:57 completed
task:58 release device
task:58 completed
task:59 release device
task:59 completed
task:60 got device. device id: 0
task:61 got device. device id: 1
task:62 got device. device id: 2
task:63 got device. device id: 3
task:64 got device. device id: 4
task:65 got device. device id: 5
task:66 got device. device id: 6
task:67 got device. device id: 7
task:68 got device. device id: 8
task:69 got device. device id: 9
task:60 release device
task:60 completed
task:61 release device
task:61 completed
task:62 release device
task:62 completed
task:63 release device
task:63 completed
task:64 release device
task:64 completed
task:65 release device
task:65 completed
task:66 release device
task:66 completed
task:67 release device
task:67 completed
task:68 release device
task:68 completed
task:69 release device
task:69 completed
task:70 got device. device id: 0
task:71 got device. device id: 1
task:72 got device. device id: 2
task:73 got device. device id: 3
task:74 got device. device id: 4
task:75 got device. device id: 5
task:76 got device. device id: 6
task:77 got device. device id: 7
task:78 got device. device id: 8
task:79 got device. device id: 9
task:70 release device
task:70 completed
task:71 release device
task:71 completed
task:72 release device
task:72 completed
task:73 release device
task:73 completed
task:74 release device
task:74 completed
task:75 release device
task:75 completed
task:76 release device
task:76 completed
task:77 release device
task:77 completed
task:78 release device
task:78 completed
task:79 release device
task:79 completed
task:80 got device. device id: 0
task:81 got device. device id: 1
task:82 got device. device id: 2
task:83 got device. device id: 3
task:84 got device. device id: 4
task:85 got device. device id: 5
task:86 got device. device id: 6
task:87 got device. device id: 7
task:88 got device. device id: 8
task:89 got device. device id: 9
task:80 release device
task:80 completed
task:81 release device
task:81 completed
task:82 release device
task:82 completed
task:83 release device
task:83 completed
task:84 release device
task:84 completed
task:85 release device
task:85 completed
task:86 release device
task:86 completed
task:87 release device
task:87 completed
task:88 release device
task:88 completed
task:89 release device
task:89 completed
task:90 got device. device id: 0
task:91 got device. device id: 1
task:92 got device. device id: 2
task:93 got device. device id: 3
task:94 got device. device id: 4
task:95 got device. device id: 5
task:96 got device. device id: 6
task:97 got device. device id: 7
task:98 got device. device id: 8
task:99 got device. device id: 9
task:90 release device
task:90 completed
task:91 release device
task:91 completed
task:92 release device
task:92 completed
task:93 release device
task:93 completed
task:94 release device
task:94 completed
task:95 release device
task:95 completed
task:96 release device
task:96 completed
task:97 release device
task:97 completed
task:98 release device
task:98 completed
task:99 release device
task:99 completed
Finished all tasks
```