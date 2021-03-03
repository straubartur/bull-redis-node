# bull-redis-node


```node
var Queue = require('bull');
const { client } = require('./cache')

redisConf = {
    host: 'localhost',
    port: 6379,
    password: null
}
const QUEUES = [
    {
        name: 'OrderVtexQueue',
        options: {
          delay: 300,
          attempts: 5
        },
        async handle(job) {
          return new Promise((resolve, reject)=>{
            try {
                //resolve(console.log(job.data))
                
            } catch (error) {
                reject(console.log(error))
            }
     
          })
        },
      }
]

const queues = QUEUES.reduce((newQueues ,queue) => {
    const cratedQueue = new Queue(queue.name, redisConf)
    console.log(cratedQueue.process, typeof cratedQueue.process)
    cratedQueue.process(queue.handle)
    return {
        [queue.name]: cratedQueue,
        ...newQueues
    }
}, {});


queues['OrderVtexQueue'].add({ tetse: '123'}, {
    delay: 300,
    attempts: 5
  })
module.exports = {
    queues
}
```
