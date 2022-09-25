
<template>
  <link
  href="https://cdnjs.cloudflare.com/ajax/libs/mdb-ui-kit/5.0.0/mdb.min.css"
  rel="stylesheet"
/>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css" />
 
  <div class="font-poppins w-full h-screen flex overflow-x-hidden flex-col   bg-[#dfdfdf]">
    <div class="mx-20 box-border relative my-auto">
      <div class="flex flex-col p-3">
        <div class="flex">
          <div class="bg-opacity-50 bg-slate-200 rounded-md backdrop-filter backdrop-blur-md shadow-md font-light text-sm ml-4 my-3 mr-3 font-poppins py-1 text-start text-slate-700 basis-1/2 pl-3 italic">Welcome, Ahnaf Musyaffa</div>
          <div class="bg-opacity-50 bg-slate-200 rounded-md backdrop-filter backdrop-blur-md shadow-md font-light text-sm mr-4 my-3 ml-3 font-poppins py-1 italic text-end pr-3 text-slate-700  basis-1/2"> 
            Digital Clock by github.com/ahnafms
          </div>
        </div>
        <div class="flex text-slate-800">
          <div class="p-2 basis-1/2 flex bg-opacity-20 backdrop-blur-md rounded-md shadow-md bg-slate-50 py-4 ml-4 mr-2">
            <div class="bg-opacity-20 basis-1/3 shadow-md ml-4 backdrop-blur-md font-helvetica bg-slate-100 rounded-xl">
                <div class="text-center">
                  <p class="mt-5">TickTock</p>
                  <p class="text-9xl">{{ dateTime.hours }}</p>
                </div>
                <div class=" flex flex-col justify-center p-10">
                  <span class="self-center text-3xl">{{ dateTime.minutes }}</span>
                  <span class="self-center text-xl">-</span>
                  <span class="self-center text-3xl">{{ dateTime.seconds }}</span>
                  <span class="self-center text-xl">-</span>
                  <span class="self-center text-xl">{{ dateTime.cons }}</span>
                </div>
              </div>
            <div class="basis-2/3 flex flex-col">
              <div class="basis-1/3 flex mb-4 px-4 bg-opacity-20 shadow-md ml-4  backdrop-blur-lg font-helvetica bg-slate-50 rounded-xl mr-4 text-center justify-evenly">
                <div class="text-6xl self-center">
                  {{ dateTime.date }} 
                </div>
                <div class="pl-4 self-center ">
                  <p class="text-lg text-start mb-0">{{ dateTime.month }} <i class="flag flag-indonesia"></i></p>
                  <p class="text-lg text-start mb-0">{{ dateTime.days }}, {{ dateTime.year }}</p>
                </div>
                <div class="self-center w-28 pl-10">
                  <i class="text-6xl fa fa-globe" aria-hidden="true"></i>
                </div>
                
              </div>
              <div class=" basis-2/3 bg-opacity-20 shadow-md ml-4 backdrop-blur-lg font-helvetica bg-slate-50 rounded-xl mr-4 text-center pt-4">Scheduled Alarm <i class="fa fa-calendar" aria-hidden="true"></i>
                 <div  v-for="(alarm, index) in myAlarm" :key="index">
                    <div class="flex justify-between px-4 py-2 self-center" >
                      <div class=" text-xl font-poppins italic">{{ myAlarm[index].activity }} </div>
                      <div class="flex" >
                        <p class="pr-4">{{ myAlarm[index].hours }} {{ myAlarm[index].minutes }} {{ myAlarm[index].cons }}</p>
                        <span v-if="myAlarm[index].isActive != null" class="flex mt-2 mr-2 h-3 w-3 justify-center">
                          <span :class="[myAlarm[index].isActive ? 'animate-ping absolute h-3 w-3 rounded-full bg-green-300 opacity-75'  : 'animate-ping absolute h-3 w-3 rounded-full bg-red-300 opacity-75' ]"></span>
                          <span :class="[myAlarm[index].isActive ?  'animate-ping relative mt-[2px] rounded-full h-2 w-2 bg-green-400' :'animate-ping relative mt-[2px] h-2 w-2 rounded-full bg-red-300 opacity-75'  ]"></span>
                        </span>
                      </div>
                      <button v-if="myAlarm[index].isActive == false" @click="removeAlarm(index)"><i class="hover:bg-red-500 hover:duration-300 rounded-full p-2 fa fa-minus" aria-hidden="true"></i></button>
                    </div>
                  </div>
              </div>
              </div>
          </div>
              
          <div class="bg-opacity-20 backdrop-blur-md shadow-md basis-1/2 text-center font-helvetica bg-slate-50 rounded-md mr-4 py-4 ml-4">
            <div class="flex justify-between px-2">
              <div class=" basis-1/2 ml-4 bg-opacity-20 backdrop-blur-lg shadow-md font-helvetica bg-slate-100 rounded-xl">
                <div class="py-5">Add Activity <i class="fa fa-trophy" aria-hidden="true"></i></div>
                <div>
                  <div class="group ">
                    <div class="group-hover:-translate-y-3 group-hover:scale-125 hover:duration-200 bg-slate-100 bg-opacity-20 rounded-lg box-border backdrop-filter backdrop-blur-md shadow-md flex justify-evenly py-2 ">
                      <input v-model="tempActivity" class="mb-2 overflow-hidden px-4 w-full bg-transparent" placeholder="Fill me!" />
                  </div>
                  </div>
                </div>
              </div>
              <div class="basis-1/2 bg-opacity-20 shadow-md ml-4 backdrop-blur-lg font-helvetica bg-slate-100 rounded-xl mr-4 text-center">
                <div class="py-5">Add Alarm </div>
                  <div class="group">
                    <div class="group-hover:-translate-y-3 group-hover:scale-125 hover:duration-200 bg-slate-100 bg-opacity-20 rounded-lg box-border backdrop-filter backdrop-blur-md shadow-md flex justify-evenly py-2">
                      <input type="time" v-model="tempAlarm" class="text-xl bg-transparent border-none">
                      <div>
                        <button type="button" @click="setAlarm()" class="box-border ">
                        <i class="hover:bg-green-500 hover:duration-300 rounded-full p-2 fa fa-arrow-up" aria-hidden="true"></i>
                        </button>
                      </div>
                    </div>
                  </div>
               </div>
            </div>
            <div class="bg-opacity-20 shadow-lg mx-4 pt-4 mt-4 text-4xl text-start px-4 h-72 backdrop-blur-md font-helvetica bg-slate-100 rounded-xl ">
              <button type="button" @click="show = !show">
                <i class="fa fa-plus hover:bg-green-500 hover:duration-300 rounded-full p-2" aria-hidden="true"></i>
              </button>
              <div v-if="show" class="text-center mt-14 text-2xl">
                Sorry, Content is not available yet.
              </div>
            </div>
          </div>
          </div>        
      </div>
      <div className="flex justify-between">
              <div className=" rounded-full -mt-80 -mx-16 w-[140px] h-[140px] bg-gradient-to-b from-[#FFF2CE] to-[#53EA90]">
                  <div className=" rounded-full w-[140px] h-[140px] bg-gradient-to-b  from-[#FFF2CE] to-[#53EA90] blur-xl"></div>    
                  </div>
              <div className=" -mt-16 rounded-full w-[160px] h-[160px] bg-gradient-to-b from-[#FFF9EE] to-[#EC6350]">
              <div className="rounded-full w-[170px] h-[170px] bg-gradient-to-b from-[#FFF9EE] to-[#EC6350] blur-xl"></div>
              </div>
          </div>
    </div>
    
  </div>
  
</template>
<style>
  .{

  }
</style>
<script>
import './assets/tailwind.css'
export default{
  data(){
    return{
      show: false,
      count: null,
      tempActivity:"",
      tempAlarm:"",
      dateTime:{
        days : '',
        hours : '',
        minutes : '',
        seconds : '',
        date: '',
        month : '',
        year: '',
        cons: '',
      },
      myAlarm:[
        {
          hours : null,
          minutes : null,
          activity: null,
          isActive: null,
          cons : ''
        },
      ],
    };
  },
  methods:{
    setAlarm(){
      this.count = this.myAlarm.length - 1
      const arr = Array.from(this.tempAlarm)
      this.myAlarm[this.count] = {
        hours: arr[0]+arr[1],
        minutes: arr[3]+arr[4],
        activity: this.tempActivity,
        isActive : true,
      }
      if (this.myAlarm[this.count].hours >= 0 && this.myAlarm[this.count].hours <= 12) this.myAlarm[this.count].cons = "AM";
      this.myAlarm[this.count].cons = "PM";
      
      this.myAlarm.push({
          hours : '',
          minutes : '',
          activity: '',
          cons : '',
      })
      console.log(this.myAlarm[this.count], this.count)
    },
    removeAlarm(index){
      this.myAlarm.splice(index, 1)
    },
    checkAlarm(){
      for(let i=0; i <= this.count; i++){
        if(this.myAlarm[i].hours == this.dateTime.hours && this.myAlarm[i].minutes == this.dateTime.minutes) this.myAlarm[i].isActive = false;
      }
    }
  },
  mounted(){
    setInterval((this.checkAlarm), 1000)
    setInterval(() => {
        var date = new Date();
        const days = ['Sunday','Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
        const months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
        this.dateTime = {
        date : date.getDate(),
        year : date.getFullYear(),
        days : days[date.getDay()],
        month : months[date.getMonth()],
        hours : date.getHours(),
        minutes : date.getMinutes(),
        seconds : date.getSeconds(),
      }
      if (this.dateTime.hours >= 0 && this.dateTime.hours <= 12){
        this.dateTime.cons = "AM";
      }
      else{
        this.dateTime.cons = "PM";
      }
    }, 1000)
  }
}
</script>

<style src="./assets/tailwind.css"/>
