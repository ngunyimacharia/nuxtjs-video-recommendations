<template>
  <div>
    <h1 class="my-10 block text-center leading-8 font-extrabold tracking-tight text-gray-600 text-2xl"> 
      How to display video recommendations in Nuxt.Js
    </h1>

      <video
        id="recommendations-player"
        controls
        muted
        class="cld-video-player cld-video-player-skin-dark w-2/3 h-96 mx-auto"
      >
      </video>
      
      <div class="mt-6 prose prose-indigo prose-lg text-gray-500 mx-auto leading-10 w-2/3 mx-auto">
        The first video will display other videos as recommendations once play ends.
      </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return {
      cld:null,
      player:null,
      source1: { 
        publicId: "nuxtjs-video-recommendations/street",
        title:'Night Street',
        subtitle:'Street at night with traffic and pedestrians',
        description:'Street at night with traffic and pedestrians'
       },
      source2: { 
        publicId: "nuxtjs-video-recommendations/cookie",
        title:'Cookie',
        subtitle:'Decorating a Cupcake with Gingerbread Cookie',
        description:'Decorating a Cupcake with Gingerbread Cookie'
       },
      source3: { 
        publicId: "nuxtjs-video-recommendations/food",
        title:'Food',
        subtitle:'Video of a Food on Table',
        description:'Video of a Food on Table'
       },
      source4: { 
        publicId: "nuxtjs-video-recommendations/plant",
        title:'plant',
        subtitle:'Close-Up of Plant With Green Leaves',
        description:'Close-Up of Plant With Green Leaves'
       },
    };
  },
  mounted(){
    this.source1.recommendations = [
      this.source2,
      this.source3,
      this.source4
    ];

    this.cld = cloudinary.Cloudinary.new({ 
      cloud_name: process.env.NUXT_ENV_CLOUDINARY_CLOUD_NAME,
      secure: true,
      transformation: {crop: 'limit', width: 300, height:900}
    });
    
    this.player = this.cld.videoPlayer('recommendations-player', 
      {
        autoShowRecommendations: true,
        sourceTypes: ['mp4']
      }
    );

    this.player.source(this.source1);
  }
}
</script>
