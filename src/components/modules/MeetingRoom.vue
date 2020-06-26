<template>
  <div id="container">
    <div class="meeting-room" id="meeting-room">
      <iframe
        v-show="iframe.hidden"
        :src="iframe.src"
        :height="height"
        :width="width"
        scrolling="no"
        frameborder="no"
        allow="geolocation;camera;microphone;"
      >
      </iframe>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MeetingRoom',
  data () {
    return {
      width: 0,
      height: 0,
      iframe: {
        src: '',
        hidden: false
      }
    }
  },
  methods: {
    setMeetingRoomSrc (src) {
      const meetingRoomSrc = this.regexZoomURL(src)
      this.iframe.src = meetingRoomSrc
      this.iframe.hidden = true
    },
    regexZoomURL (url) {
      console.log(url)
      const reg = /(\/j\/)(\d*)\?pwd=(.*)/
      const urlDetail = url.match(reg)
      const zoomPWDNumber = urlDetail[2]
      const zoomPWD = urlDetail[3]
      const zoomRoomURL = 'https://us04web.zoom.us/wc/join/' + zoomPWDNumber + '?wpk=' + zoomPWD
      return zoomRoomURL
    },
    handleResize () {
      // resizeのたびにこいつが発火するので、ここでやりたいことをやる
      // this.width = window.innerWidth
      // this.height = window.innerHeight
    },
    iframeResize (height, width) {
      this.height = height
      this.width = width
    }
  },
  mounted () {
    window.addEventListener('resize', this.handleResize)
    console.log('画面全体の高さ: ' + this.height)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.handleResize)
  }
}
</script>

<style scoped>
body,
html {
  margin: 0;
  padding: 0;
}

#container {
}

body {
  font-family: 'Source Sans Pro', sans-serif;
  /* font-size: 18px; */
}

.meeting-room {
  background-color: aliceblue;
}

iframe {
  vertical-align: bottom;
  border:none;
  box-sizing : border-box;
  font-weight: bold;
  border: solid 1px #000000;
}
</style>
