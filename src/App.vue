<template>
	<h1>Курс</h1>

	<button class="restoreBtn" @click="restoreWatchedVideos">Сбросить просмотренные видео</button>

	<div 
		class="video"
		:class="{'watched': idx + 1 <= watchedIndex}"
		v-for="(video, idx) in courseList" 
		:key="idx"
	>
		<div class="rowBtns">
		<h2>Видео № {{ idx + 1 }}</h2>
		<button class="checkWatched" @click="watched(idx + 1)">Отметить просмотренным</button>
	</div>

		<video controls>
			<source :src="video.src">
		</video>
	</div>
</template>

<script>
import courseList from './course';

export default {
	data() {
		return {
			lessonsLength: 5,
			courseList: courseList,
			storageKey: 'courseIndx',
			watchedIndex: null,
		}
	},

	mounted() {
		this.watchedIndex = localStorage.getItem(this.storageKey)
	},

	methods: {
		watched(index) {
			localStorage.setItem(this.storageKey, index)
			this.watchedIndex = localStorage.getItem(this.storageKey)
			document.location.reload()
		},

		restoreWatchedVideos() {
			localStorage.removeItem(this.storageKey)
			this.watchedIndex = null
			document.location.reload()
		}
	}
}
</script>

<style lang="scss">
* {
	margin: 0;
	padding: 0;
	font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}

body {
	background: #101214;
	color: #DEE4EA;
}

h1 {
	text-align: center;
	font-size: 50px;
}

button {
	background: #DEE4EA;
	outline: none;
	border-radius: 10px;
	font-size: 16px;
	font-weight: 600;
	padding: 10px 30px;
	border: none;
	transition: all .25s ease;
	cursor: pointer;

	&:hover {
		background: tomato;
	}
}

.restoreBtn {
	display: block;
	margin: 5px auto;
}

.video {
	width: 60%;
	margin: 20px auto;
	
	.rowBtns {
		display: flex;
		align-items: center;
		justify-content: space-between;
		margin-bottom: 5px;
	}

	video {
		width: 100%;
		border-radius: 10px;
		border: 2px solid #DEE4EA;
	}
}

.video.watched {
	display: none;
}
</style>
