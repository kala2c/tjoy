<style>
  .rect,
  .circle {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    border: 1px solid #eee;
  }
  .rect {
    border-radius: 6rpx;
  }
  .circle {
    border-radius: 50%;
  }
  uni-page-body {
    position: relative;
    height: 100%;
  }
  .content {
    width: 100%;
    position: absolute;
  }
  .key {
    position: absolute;
  }
</style>

<template>
	<view class="content" :style="{ height: containerH, top: containerTop}">
    <view
        v-for="key in keyMap"
        :key="key.id"
        class="key"
        :class="key.face.shape === 'rect' ? 'rect' : 'circle'"
        :style="{
          top: key.seat.y * sizeRate  + 'px',
          left: key.seat.x * sizeRate + 'px',
          width: key.face.width * sizeRate + 'px',
          height: key.face.height * sizeRate + 'px',
          borderColor: key.face.borderColor,
          color: key.face.color,
          backgroundColor: key.face.backgroundColor
        }"
    >
      {{ key.content }}
    </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
        containerH: '550px',
        containerTop: 0,
        sizeRate: 3.75,
        keyMap: [
          {
            id: '11',
            face: {
              width: 10,
              height: 10,
              shape: 'circle',
              borderColor: '#666',
              color: '#333',
              backgroundColor: '#eee'
            },
            seat: {
              x: 10,
              y: 20
            },
            content: 'A'
          },
          {
            id: '2',
            face: {
              width: 10,
              height: 10,
              shape: 'rect',
              borderColor: '#666',
              color: '#333',
              backgroundColor: '#eee'
            },
            seat: {
              x: 30,
              y: 20
            },
            content: 'B'
          }
        ]
			}
		},
		onLoad() {
		  const _this = this
      uni.getSystemInfo({
        success: function (info) {
          const width = info.windowWidth
          const totalHeight = info.windowHeight
          const pixelRatio = info.pixelRatio
          const height = Math.ceil(width*1.6)
          _this.containerH = Math.ceil(width*1.6) + 'px'
          _this.containerTop = (totalHeight - height)/2 + 'px'
          _this.sizeRate = width/100
        },
        fail: function () {
          uni.showToast({
            message: '初始化失败！'
          })
        }
      })
		},
		methods: {

		}
	}
</script>
