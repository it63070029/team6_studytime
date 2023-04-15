<template>
    <div class="container is-widescreen">
     
      <section class="section" id="app">
        <div class="content">
          <!-- <div class="columns"> -->
            <center><h1>รายการแจ้งเตือน</h1></center>
            <div class="column is-6 " style="margin-left:25%; " >
              <div v-for="subjectnews in newsTotal" :key="subjectnews.id" class="card mb-3 ">
                <div  :style="{'background-color':subjectnews.bgSuccess?'#2B3467':'#BAD7E9'}">
                
                <div class="card-content ">
                 
                 
                  <h4  style="color:#FFF;"> 
                    <span class="icon" v-if="!subjectnews.bgSuccess">
                        <i class="fa fa-circle"></i>
                    </span>
                    <span class="icon" v-if="subjectnews.bgSuccess">
                        <i class="fa fa-check-circle"></i>
                    </span>
                    {{subjectnews.topic}}</h4>
                  <h6 style="color:#FFF;margin-bottom:10px">โดย : {{subjectnews.teach}}</h6>
                  
                  <div style="color:#FFF">วันที่: {{subjectnews.date +"  เวลา: "+ subjectnews.time+" น."}}<span style="float:right"><div class="button" @click="showDetail(subjectnews.id)">ดูเพิ่มเติม > </div></span></div>
                
                </div></div>
                 
                  
                
              </div>
            </div>
          <!-- </div> -->
        </div>
    
  
         <!-- Modal Show DetailSubject -Start -->
        <div class="modal" :class="{'is-active': modalShowDetail}" >
          <div class="modal-background"></div>
          <div class="modal-card" v-for="(subjectnews,index) in selectnews" :key="subjectnews.id">
            <header class="modal-card-head">
              <p class="modal-card-title">{{subjectnews.topic}}</p>
              <button class="delete" aria-label="close" @click=" modalShowDetail=false"></button>
            </header>
            <section class="modal-card-body">
              <!-- Content ... -->
             
             
              <div class="columns" style="margin-bottom: 20px;">
                <h1>รายละเอียดราย : {{subjectnews.detail}}</h1>
              </div>
               <div class="columns" style="margin-bottom: 20px;">
                <div>อาจารย์ผู้สอน : {{subjectnews.teach}}</div>
              </div>
               <div class="columns" style="margin-bottom: 20px;">
                <div>วันที่ : {{ subjectnews.date }}</div>
              </div>
              
               <div class="columns" style="margin-bottom: 20px;"> 
                <div>เวลา : {{ subjectnews.time }} </div>
              </div>
              
              <div class="button" v-if="!selectnews.bgSuccess" @click="confirmNews(index)" > ยืนยันทราบข่าวสาร </div>
              
            </section>
            
          </div>
        </div>
        <!-- Modal Add -End -->
      </section>
        
    </div>
  
   
  </template>
  
  <script>
  import axios from "axios";
  // @ is an alias to /src
  export default {
    name: "newsofsubject",
    // props: ['user'],
    data() {
      return {
        selectnews_subject:[],
        newsTotal:[
            {id:1,idSubject:"06016310",teach:"รศ.ดร.นพพร โชติกกำธร",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"20/11/65",time:"8.45",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนเวลาที่ทำการเรียนการสอนเป็น 14.30-16.30 น.",bgSuccess:false},
            {id:2,idSubject:"06016310",teach:"รศ.ดร.นพพร โชติกกำธร",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"12/11/65",time:"10.05",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนสถานที่ที่ทำการสอนเป็น project base 3",bgSuccess:true},
            {id:3,idSubject:"06016325",teach:"ผศ.ดร. ธราวิเชษฐ์ ธิติจรูญโรจน์",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"20/11/65",time:"7.00",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนเวลาที่ทำการเรียนการสอนเป็น 14.30-16.30 น.",bgSuccess:false},
                  {id:4,idSubject:"06016323",teach:"ดร. พัฒนพงษ์ ฉันทมิตรโอภาส",topic:"งดการเรียน",date:"21/11/65",time:"13.00",detail:"งดการเรียนเนื่องการสถานการณืน้ำท่วม",bgSuccess:false},
            {id:6,idSubject:"06016323",teach:"ดร. พัฒนพงษ์ ฉันทมิตรโอภาส",topic:"การสอนชดเชย",date:"23/11/65",time:"13.00",detail:"สอนชดเชยจากคาบที่แล้ว ที่ห้องL307",bgSuccess:false},
            {id:8,idSubject:"06016323",teach:"ดร. พัฒนพงษ์ ฉันทมิตรโอภาส",topic:"การส่งงาน", date:"24/11/65",time:"12.00",detail:"ให้นักศึกษาส่งงานที่ onlearn ภายในวันที่ 26/11/65 เวลา 23.59 น.",bgSuccess:false},
            {id:5,idSubject:"90304004",teach:"ผศ. จันจิรา จันทร์เจริญสุข",topic:"งดการเรียน",date:"19/10/65",time:"9.00",detail:"งดการเรียนการสอนเนื่องจากฝุ่น PM2.5มีปริมาณมาก",bgSuccess:false},
            {id:7,idSubject:"06016309",teach:"ผศ.ดร. สุเมธ ประภาวัต",topic:"การส่งงาน", date:"20/11/65",time:"15.00",detail:"ให้นักศึกษาส่งงานที่ onlearn ภายในวันที่ 22/11/65 เวลา 23.59 น.",bgSuccess:false},
            {id:10,idSubject:"06016309",teach:"ผศ.ดร. สุเมธ ประภาวัต",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"16/11/65",time:"11.00",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนสถานที่ที่ทำการสอนเป็น M22",bgSuccess:false},
            {id:9,idSubject:"06016319",teach:"ผศ.ดร. สุภกิจ นุตยะสกุล",topic:"การเปลี่ยนแปลงสถานที่เรียน",date:"14/11/65",time:"15.00",detail:"เนื่องด้วยปัญหาทางเทคนิคจึงขอเปลี่ยนสถานที่ที่ทำการสอนเป็น M21",bgSuccess:false},

        ],
        modalShowDetail:false,
        selectnews:[],
        
        
    
  
      };
    },
    mounted() {
      
    },
    methods: {
      confirmNews(index){
        this.modalShowDetail =false
        console.log(index)
        this.newsTotal[index].bgSuccess = true

        
      },
      showDetail(id){
        this.modalShowDetail = true;
        this.selectnews = this.newsTotal.filter((val)=>(val.id==id))
       
      },
    
    },
  };
  </script>
  
