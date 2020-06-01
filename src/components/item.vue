<template>
	<div class = "gallery-pills"
	v-bind:class ="{left:image.position_left, center:image.position_center, right:image.position_right}"
	>
		<img id="img" v-on:click="$emit('clickimg',image.id)":src=image.src>
		<img id="X" v-on:click="$emit('clickimg',-image.id)"src="image/X.png" v-bind:class ="{xnotActive1:image.position_right, xnotActive2:image.position_left, XZ:image.position_center}">
	</div>
</template>

<script>

export default 
{
	props:{
		image:{	
			type: Object,
			required: true
		}
	}
}
</script>

<style scoped>
.gallery-pills {
    margin: 1rem;
    right: 4rem;
    width: 250px;
    height: 325px;
    display: inline-block;
    box-shadow: 0 0 0 2px #00f9f9, 0 0 0 3px #fc0201, 0 0 0 5px #474347;
}
.center{
	position: fixed;
	width: 100vw;
	height: 100vh;
	z-index: 1;
	margin:0;
	right: 0;
}
.center #img{
	height: 100vh;
  width: 100vw;
  object-fit: contain;
  animation: unfoldIn 1s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}

div.left, div.right{
	position: fixed;
	z-index: 2;
	margin:0;
	padding: 0;
	opacity: 0.75;
	height: 14vw;
	width: 10vw;
}
.left{
	left: 0;
	animation: unfoldIn 1s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}
.right{
	right: 0;
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
img
{
	height: 325px;
  width: 250px;
}
div.left img, div.right img{
	height: 14vw;
	width: 10vw;
}
#X{
	position: relative;
	height: 50px;
	width: 50px;
	left: 100px;
	bottom: 330px;
}
#X.XZ{
	position: absolute;
	height: 10vh;
	width: 10vh;
	z-index: 10;

	left: calc(50vw - 5vh);
	top: 0;
	animation: unfoldIn 1s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}
.xnotActive1,.xnotActive2 
{
	display: none;
}

</style>