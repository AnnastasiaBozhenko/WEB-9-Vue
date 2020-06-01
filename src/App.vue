<template>
  <div id="app">
    <div id="modal-container" style="display: none;">
      <div id="modal-back"></div>
      <Items v-bind:image = "image_left"   v-on:clickimg="clickimg"/>
      <Items v-bind:image = "image_center" v-on:clickimg="clickimg"/>
      <Items v-bind:image = "image_right"  v-on:clickimg="clickimg"/>
    </div>
    <div id="header">
      <form
        enctype="multipart/form-data">
        <input type="file" @change ="AddImage" multiple accept="image/*,image/jpeg">
      </form>
    </div>
    <List_image v-bind:List_img="List_img" v-on:clickimg="clickimg"/>
  </div>
</template>

<script>
import List_image from '@/components/list_img.vue'
import Items from '@/components/item'
export default {
  name: 'App',
  data() {
    return {
      List_img: [
      {id:1,position_center:false,position_left:false,position_right:false,src:"image/1.jpg"},
      {id:2,position_center:false,position_left:false,position_right:false,src:"image/2.jpg"},
      {id:3,position_center:false,position_left:false,position_right:false,src:"image/3.jpg"},
      {id:4,position_center:false,position_left:false,position_right:false,src:"image/4.png"},
      {id:5,position_center:false,position_left:false,position_right:false,src:"image/5.jpg"},
      {id:6,position_center:false,position_left:false,position_right:false,src:"image/6.jpg"},
      {id:7,position_center:false,position_left:false,position_right:false,src:"image/7.jpg"}
      ],
      zoom:false,
      ID:7,

      image_center:{},
      image_left:{},
      image_right:{}
    }
  },
  methods: 
  {
    clickimg(id)
    {
      if(!this.zoom)
      {
        if(id >= 0)
        {
          document.getElementById("modal-container").style["display"] = "flex";
          this.zoom = true;
          for (let i = 0; i < this.List_img.length; i++)
          {
            if(this.List_img[i].id == id)
            {
              const l = this.List_img[((i)?(i-1):this.List_img.length-1)];
              const r = this.List_img[((i == this.List_img.length-1)?0:(i+1))];

              this.image_left = {id:l.id,position_center:false,position_left:true,position_right:false,src:l.src};
              this.image_center = {id:this.List_img[i].id,position_center:true,position_left:false,position_right:false,src:this.List_img[i].src};
              this.image_right  = {id:r.id,position_center:false,position_left:false,position_right:true,src: r.src};
            }
          }
        }else
          this.List_img = this.List_img.filter(t => t.id != -id);
      }
      else
      {
        if(id < 0)
        {
          document.getElementById("modal-container").style["display"] = "none";
          this.zoom = false;

        }else if (id != -1){
          this.zoom = false;
          this.clickimg(id);
        }
      }
    },
    AddImage: function(e)
    {
      let file = e.target.files[0];
      let reader = new FileReader();
      reader.addEventListener('load',event=>
      {
        this.List_img.push({id:++(this.ID),position_center:false,position_left:false,position_right:false,src:event.target.result});
      });
      reader.readAsDataURL(file);
    }

  },
  components: {
    List_image,
    Items
  }
}
</script>
<style>
html,
body {
    min-height: 100%;
    background-size: cover;
    background-position: top center;
    font-weight: 200;
    background-image: url('/image/backG.jpg');
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
    text-align: center;
    max-width: 100%;
}
#modal-container{
  flex-wrap: wrap;
  align-items: center;

  right: 0;
  bottom: 0;
  top: 0;
  left: 0;
  position: absolute;
}
#modal-back{
  position: fixed;
  opacity:70%;
  background-color: #000;
  right: 0;
  bottom: 0;
  top:0;
  left:0;
  width: 100%;
  height: 100%;
  animation: unfoldIn 1s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}
@keyframes unfoldIn {
    0% {
        transform: scaleY(0.005) scaleX(0);
    }
    50% {
        transform: scaleY(0.005) scaleX(1);
    }
    100% {
        transform: scaleY(1) scaleX(1);
    }
}
form{
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000;
  width: 350px;
  height: 5vh;
  box-shadow: 0 0 0 2px #00f9f9, 0 0 0 3px #fc0201, 0 0 0 5px #474347;
}
input{
  color: white;
}
</style>
