<template>
<div class='sidebar'>
  <sidebar-menu
    :menu="menu"
    :collapsed="collapsed"
    @item-click="onItemClick"
    >
  </sidebar-menu>

  <splitpanes
    style="height: 100vh; padding-left: 50px;"
    class="default-theme"
    horizontal
    @resized="iframeResize()"
    @resize="iframeResize()"
  >
    <pane :size="size">
      <splitpanes
        @resized="iframeResize()"
        @resize="iframeResize()"
      >
        <pane id="meetingRoom" min-size="30">
          <span>
            <div v-show="roomIcon">
              <svg id="icon" @click="openLinkModal()" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="link" class="svg-inline--fa fa-link fa-w-16" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M326.612 185.391c59.747 59.809 58.927 155.698.36 214.59-.11.12-.24.25-.36.37l-67.2 67.2c-59.27 59.27-155.699 59.262-214.96 0-59.27-59.26-59.27-155.7 0-214.96l37.106-37.106c9.84-9.84 26.786-3.3 27.294 10.606.648 17.722 3.826 35.527 9.69 52.721 1.986 5.822.567 12.262-3.783 16.612l-13.087 13.087c-28.026 28.026-28.905 73.66-1.155 101.96 28.024 28.579 74.086 28.749 102.325.51l67.2-67.19c28.191-28.191 28.073-73.757 0-101.83-3.701-3.694-7.429-6.564-10.341-8.569a16.037 16.037 0 0 1-6.947-12.606c-.396-10.567 3.348-21.456 11.698-29.806l21.054-21.055c5.521-5.521 14.182-6.199 20.584-1.731a152.482 152.482 0 0 1 20.522 17.197zM467.547 44.449c-59.261-59.262-155.69-59.27-214.96 0l-67.2 67.2c-.12.12-.25.25-.36.37-58.566 58.892-59.387 154.781.36 214.59a152.454 152.454 0 0 0 20.521 17.196c6.402 4.468 15.064 3.789 20.584-1.731l21.054-21.055c8.35-8.35 12.094-19.239 11.698-29.806a16.037 16.037 0 0 0-6.947-12.606c-2.912-2.005-6.64-4.875-10.341-8.569-28.073-28.073-28.191-73.639 0-101.83l67.2-67.19c28.239-28.239 74.3-28.069 102.325.51 27.75 28.3 26.872 73.934-1.155 101.96l-13.087 13.087c-4.35 4.35-5.769 10.79-3.783 16.612 5.864 17.194 9.042 34.999 9.69 52.721.509 13.906 17.454 20.446 27.294 10.606l37.106-37.106c59.271-59.259 59.271-155.699.001-214.959z"></path></svg>
            </div>
            <meeting-room ref="meetingRoom"></meeting-room>
          </span>
        </pane>
        <!-- 上のパネル操作 -->
        <pane size=30 class="panes" v-for="upperPaneN in upperPaneNumber" :key="upperPaneN">
          <div v-show="upperPane[upperPaneN-1].icon">
            <p>{{ upperPaneN }}</p>
            <svg id="icon" @click="openPaneModal(upperPane[upperPaneN-1].id, 'upper')" aria-hidden="true" focusable="false" data-prefix="far" data-icon="plus-square" class="svg-inline--fa fa-plus-square fa-w-14" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M352 240v32c0 6.6-5.4 12-12 12h-88v88c0 6.6-5.4 12-12 12h-32c-6.6 0-12-5.4-12-12v-88h-88c-6.6 0-12-5.4-12-12v-32c0-6.6 5.4-12 12-12h88v-88c0-6.6 5.4-12 12-12h32c6.6 0 12 5.4 12 12v88h88c6.6 0 12 5.4 12 12zm96-160v352c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V80c0-26.5 21.5-48 48-48h352c26.5 0 48 21.5 48 48zm-48 346V86c0-3.3-2.7-6-6-6H54c-3.3 0-6 2.7-6 6v340c0 3.3 2.7 6 6 6h340c3.3 0 6-2.7 6-6z"></path></svg>
            <!-- <svg id="icon" @click="openPaneModal(upperPane[upperPaneN-1].id, 'upper')" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="cog" class="svg-inline--fa fa-cog fa-w-16" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M487.4 315.7l-42.6-24.6c4.3-23.2 4.3-47 0-70.2l42.6-24.6c4.9-2.8 7.1-8.6 5.5-14-11.1-35.6-30-67.8-54.7-94.6-3.8-4.1-10-5.1-14.8-2.3L380.8 110c-17.9-15.4-38.5-27.3-60.8-35.1V25.8c0-5.6-3.9-10.5-9.4-11.7-36.7-8.2-74.3-7.8-109.2 0-5.5 1.2-9.4 6.1-9.4 11.7V75c-22.2 7.9-42.8 19.8-60.8 35.1L88.7 85.5c-4.9-2.8-11-1.9-14.8 2.3-24.7 26.7-43.6 58.9-54.7 94.6-1.7 5.4.6 11.2 5.5 14L67.3 221c-4.3 23.2-4.3 47 0 70.2l-42.6 24.6c-4.9 2.8-7.1 8.6-5.5 14 11.1 35.6 30 67.8 54.7 94.6 3.8 4.1 10 5.1 14.8 2.3l42.6-24.6c17.9 15.4 38.5 27.3 60.8 35.1v49.2c0 5.6 3.9 10.5 9.4 11.7 36.7 8.2 74.3 7.8 109.2 0 5.5-1.2 9.4-6.1 9.4-11.7v-49.2c22.2-7.9 42.8-19.8 60.8-35.1l42.6 24.6c4.9 2.8 11 1.9 14.8-2.3 24.7-26.7 43.6-58.9 54.7-94.6 1.5-5.5-.7-11.3-5.6-14.1zM256 336c-44.1 0-80-35.9-80-80s35.9-80 80-80 80 35.9 80 80-35.9 80-80 80z"></path></svg> -->
          </div>
          <component :is="upperPane[upperPaneN-1].loadPage"></component>
        </pane>

      </splitpanes>
    </pane>

    <!-- 下のパネル操作 -->
    <pane :size="100-size">
      <splitpanes>
        <pane class="panes" v-for="underPaneN in underPaneNumber" :key="underPaneN">
          <div v-show="underPane[underPaneN-1].icon">
            <p>{{ underPaneN }}</p>
            <svg id="icon" @click="openPaneModal(underPane[underPaneN-1].id, 'under')" aria-hidden="true" focusable="false" data-prefix="far" data-icon="plus-square" class="svg-inline--fa fa-plus-square fa-w-14" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="currentColor" d="M352 240v32c0 6.6-5.4 12-12 12h-88v88c0 6.6-5.4 12-12 12h-32c-6.6 0-12-5.4-12-12v-88h-88c-6.6 0-12-5.4-12-12v-32c0-6.6 5.4-12 12-12h88v-88c0-6.6 5.4-12 12-12h32c6.6 0 12 5.4 12 12v88h88c6.6 0 12 5.4 12 12zm96-160v352c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V80c0-26.5 21.5-48 48-48h352c26.5 0 48 21.5 48 48zm-48 346V86c0-3.3-2.7-6-6-6H54c-3.3 0-6 2.7-6 6v340c0 3.3 2.7 6 6 6h340c3.3 0 6-2.7 6-6z"></path></svg>
            <!-- <svg id="icon" @click="openPaneModal(underPane[underPaneN-1].id, 'under')" aria-hidden="true" focusable="false" data-prefix="fas" data-icon="cog" class="svg-inline--fa fa-cog fa-w-16" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M487.4 315.7l-42.6-24.6c4.3-23.2 4.3-47 0-70.2l42.6-24.6c4.9-2.8 7.1-8.6 5.5-14-11.1-35.6-30-67.8-54.7-94.6-3.8-4.1-10-5.1-14.8-2.3L380.8 110c-17.9-15.4-38.5-27.3-60.8-35.1V25.8c0-5.6-3.9-10.5-9.4-11.7-36.7-8.2-74.3-7.8-109.2 0-5.5 1.2-9.4 6.1-9.4 11.7V75c-22.2 7.9-42.8 19.8-60.8 35.1L88.7 85.5c-4.9-2.8-11-1.9-14.8 2.3-24.7 26.7-43.6 58.9-54.7 94.6-1.7 5.4.6 11.2 5.5 14L67.3 221c-4.3 23.2-4.3 47 0 70.2l-42.6 24.6c-4.9 2.8-7.1 8.6-5.5 14 11.1 35.6 30 67.8 54.7 94.6 3.8 4.1 10 5.1 14.8 2.3l42.6-24.6c17.9 15.4 38.5 27.3 60.8 35.1v49.2c0 5.6 3.9 10.5 9.4 11.7 36.7 8.2 74.3 7.8 109.2 0 5.5-1.2 9.4-6.1 9.4-11.7v-49.2c22.2-7.9 42.8-19.8 60.8-35.1l42.6 24.6c4.9 2.8 11 1.9 14.8-2.3 24.7-26.7 43.6-58.9 54.7-94.6 1.5-5.5-.7-11.3-5.6-14.1zM256 336c-44.1 0-80-35.9-80-80s35.9-80 80-80 80 35.9 80 80-35.9 80-80 80z"></path></svg> -->
          </div>
          <component :is="underPane[underPaneN-1].loadPage"></component>
        </pane>
      </splitpanes>
    </pane>

  </splitpanes>

  <LinkModalForm @close="closeLinkModal" v-if="linkModal">
    <p>共有URLを入力してください</p>
    <input class="form-control" type="text" placeholder="共有URL" v-model="shareURL">
    <template slot="footer">
      <button class="btn btn-primary" @click="setSrc(shareURL)">表示する</button>
    </template>
  </LinkModalForm>

  <PaneModalForm @close="closePaneModal" v-if="paneModal">
    <p>Pane用のモーダルです</p>
    <ul class="list-group">
      <li
        class="list-group-item"
        @click="paneItemClick($event, paneItem, paneTargetPlace, paneTarget)"
        v-for="paneItem in paneItems"
        :key="paneItem.id"
      >
        {{ paneItem.page }}
      </li>
    </ul>
  </PaneModalForm>

  <OptionModalForm @close="closeOptionModal" v-if="optionModal">
    <button @click="deletePane(paneTarget, paneTargetPlace)">削除</button>
    <button @click="changePane(paneTarget)">ページ変更</button>
  </OptionModalForm>

</div>
</template>
<script>
import { SidebarMenu } from 'vue-sidebar-menu'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faUserSecret } from '@fortawesome/free-solid-svg-icons'
import MeetingRoom from './../modules/MeetingRoom.vue'
import LinkModalForm from './../modules/LinkModalForm.vue'
import PaneModalForm from './../modules/PaneModalForm.vue'
import OptionModalForm from './../modules/OptionModalForm.vue'
import { Splitpanes, Pane } from 'splitpanes'
import TestPage1 from './../pages/TestPage1.vue'
import TestPage2 from './../pages/TestPage2.vue'
import 'splitpanes/dist/splitpanes.css'

library.add(faUserSecret)

export default {
  name: 'Sidebar',
  components: {
    SidebarMenu,
    MeetingRoom,
    LinkModalForm,
    PaneModalForm,
    OptionModalForm,
    Splitpanes,
    Pane,
    TestPage1,
    TestPage2
  },
  data () {
    return {
      linkModal: false, // Link設定用のモーダル
      paneModal: false, // pane設定用のモーダル
      optionModal: false,
      paneHidden: false,
      shareURL: '',
      roomIcon: true,
      paneTarget: 0,
      paneTargetPlace: '',
      size: 70,
      width: 0,
      upperPaneNumber: 1, // 上のpaneの枚数
      underPaneNumber: 1, // 下のpaneの枚数
      paneItems: [ // paneに設定できるページを設定する
        { id: 1, page: TestPage1.name },
        { id: 2, page: TestPage2.name }
      ],
      pane: [
      ],
      upperPane: [],
      underPane: [],
      paneNextId: 0,
      upperPaneNextId: 0,
      underPaneNextId: 0,
      menu: [
        {
          header: true,
          title: 'Items',
          hiddenOnCollapse: true
        },
        {
          title: 'Set Link',
          name: 'setLink',
          icon: 'fa fa-link',
          badge: {
            text: '共有リンクをセットします'
          }
        },
        {
          title: 'Display Raito',
          name: 'display',
          icon: 'fa fa-solar-panel',
          child: [
            {
              title: '上のパネルを追加',
              name: 'upperPanelPlus'
            },
            {
              title: '上のパネルを削除',
              name: 'upperPanelMinus'
            },
            {
              title: '下のパネルを追加',
              name: 'underPanelPlus'
            },
            {
              title: '下のパネルを削除',
              name: 'underPanelMinus'
            }
          ]
        },
        {
          title: 'Option',
          name: 'options',
          icon: 'fa fa-plus',
          child: [
            {
              title: 'Upper Pane',
              child: [
              ]
            },
            {
              title: 'Under Pane',
              child: [
              ]
            }
          ]
        }

      ],
      collapsed: true
    }
  },
  methods: {
    onItemClick (event, item) {
      console.log(item.name)
      switch (item.name) {
        case 'setLink':
          this.openLinkModal()
          break

        case 'upperPanelPlus':
          this.upperPaneNumber++
          this.addPane(this.upperPaneNextId, 'upper')
          break
        case 'upperPanelMinus':
          if (this.upperPaneNumber < 1) {
            alert('これ以上少なくできません')
            return -1
          }
          this.upperPane.splice(this.upperPaneNextId, 1)
          this.upperPaneNextId--
          this.menu[3].child[0].child.splice(this.upperPaneNextId, 1)
          this.upperPaneNumber--
          break
        case 'underPanelPlus':
          this.underPaneNumber++
          this.addPane(this.underPaneNextId, 'under')
          break
        case 'underPanelMinus':
          if (this.underPaneNumber < 1) {
            alert('これ以上少なくできません')
            return -1
          }
          this.underPane.splice(this.underPaneNextId, 1)
          this.underPaneNextId--
          this.menu[3].child[1].child.splice(this.underPaneNextId, 0)
          this.underPaneNumber--
          break
        case 'option':
          this.openOptionModal(item.id, item.place)
          break
      }
    },
    openLinkModal () {
      this.linkModal = true
    },
    closeLinkModal () {
      this.linkModal = false
    },
    openPaneModal (target, place) {
      console.log('Pane Target: ', target)
      this.paneTarget = target
      this.paneTargetPlace = place
      this.paneModal = true
    },
    closePaneModal () {
      this.paneModal = false
    },
    openOptionModal (target, place) {
      console.log('Option Target: ', target)
      this.paneTarget = target
      this.paneTargetPlace = place
      this.optionModal = true
    },
    closeOptionModal () {
      this.paneTarget = 0
      this.optionModal = false
    },
    setSrc (src) {
      this.$refs.meetingRoom.setMeetingRoomSrc(src)
      this.roomIcon = false
      const nodes = document.getElementById('meetingRoom')
      const height = window.getComputedStyle(nodes).height
      const width = window.getComputedStyle(nodes).width
      this.$refs.meetingRoom.iframeResize(height, width)
      this.closeLinkModal()
    },
    iframeResize () {
      const nodes = document.getElementById('meetingRoom')
      const height = window.getComputedStyle(nodes).height
      const width = window.getComputedStyle(nodes).width
      this.$refs.meetingRoom.iframeResize(height, width)
      console.log('meetingRoom: ' + height, width)
    },
    paneItemClick (event, item, place, paneIndex) {
      if (place === 'upper') {
        switch (item.page) {
          case TestPage1.name:
            this.upperPane[paneIndex].loadPage = TestPage1.name
            break
          case TestPage2.name:
            this.upperPane[paneIndex].loadPage = TestPage2.name
            break
        }
        this.menu[3].child[0].child[paneIndex].title = 'Pane ID: ' + (paneIndex + 1)
        this.upperPane[paneIndex].icon = false
      } else if (place === 'under') {
        switch (item.page) {
          case TestPage1.name:
            this.underPane[paneIndex].loadPage = TestPage1.name
            break
          case TestPage2.name:
            this.underPane[paneIndex].loadPage = TestPage2.name
            break
        }
        this.menu[3].child[1].child[paneIndex].title = 'Pane ID: ' + (paneIndex + 1)
        this.underPane[paneIndex].icon = false
      }
      this.closePaneModal()
    },
    // paneを追加したときに呼び出す関数
    addPane (paneId, place) {
      if (place === 'upper') {
        console.log('upper Side Init')
        this.upperPane.splice(paneId, 1,
          {
            id: paneId,
            title: 'Pane ID: ' + (paneId + 1),
            loadPage: '',
            place: 'upper',
            icon: true
          }
        )
        this.menu[3].child[0].child.splice(paneId, 1,
          {
            id: paneId,
            title: this.upperPane[paneId].title,
            loadPage: this.upperPane[paneId].loadPage,
            place: this.upperPane[paneId].place,
            name: 'option'
          }
        )
        this.upperPaneNextId++
      } else if (place === 'under') {
        console.log('under Side Init')
        this.underPane.splice(paneId, 1,
          {
            id: paneId,
            title: 'Pane ID: ' + (paneId + 1),
            loadPage: '',
            place: 'under',
            icon: true
          }
        )
        this.menu[3].child[1].child.splice(paneId, 1,
          {
            id: paneId,
            title: this.underPane[paneId].title,
            loadPage: this.underPane[paneId].loadPage,
            place: this.underPane[paneId].place,
            name: 'option'
          }
        )
        this.underPaneNextId++
      }
    },
    deletePane (paneId, place) {
      if (place === 'upper') {
        console.log('delete upper: ' + paneId)
        delete this.upperPane[paneId]
        delete this.menu[3].child[0].child[paneId]
        for (let i = paneId; i < this.upperPaneNextId; i++) {
          this.$set(this.upperPane, i, this.upperPane[i + 1])
          this.$set(this.menu[3].child[0].child, i, this.menu[3].child[0].child[i + 1])
        }
        this.upperPane.length--
        this.menu[3].child[0].child.length--
        for (let j = paneId; j < this.menu[3].child[0].child.length; j++) {
          this.upperPane[j].id--
          this.menu[3].child[0].child[j].id--
          this.menu[3].child[0].child[j].title = 'Pane ID: ' + (this.menu[3].child[0].child[j].id + 1)
        }
        this.upperPaneNextId--
        this.upperPaneNumber--
      } else if (place === 'under') {
        console.log('delete under: ' + paneId)
        delete this.underPane[paneId]
        delete this.menu[3].child[1].child[paneId]
        for (let i = paneId; i < this.underPaneNextId; i++) {
          this.$set(this.underPane, i, this.underPane[i + 1])
          this.$set(this.menu[3].child[1].child, i, this.menu[3].child[1].child[i + 1])
        }
        this.underPane.length--
        this.menu[3].child[1].child.length--
        for (let j = paneId; j < this.menu[3].child[1].child.length; j++) {
          this.underPane[j].id--
          this.menu[3].child[1].child[j].id--
          this.menu[3].child[1].child[j].title = 'Pane ID: ' + (this.menu[3].child[1].child[j].id + 1)
        }
        this.underPaneNextId--
        this.underPaneNumber--
      }
      this.closeOptionModal()
    },
    handleResize () {
      // resizeのたびにこいつが発火するので、ここでやりたいことをやる
      this.width = window.innerWidth
      this.height = window.innerHeight
    }
  },
  beforeMount () {
    // 上側の初期パネルの作成
    for (let upperN = 0; upperN < this.upperPaneNumber; upperN++) {
      this.addPane(this.upperPaneNextId, 'upper')
    }
    // 下側の初期パネルの作成
    for (let underN = 0; underN < this.underPaneNumber; underN++) {
      this.addPane(this.underPaneNextId, 'under')
    }
  },
  mounted () {
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.handleResize)
  }
}
</script>
<style lang="scss" scoped>
.game-zone {
  width: 100%;
  position: absolute;
  bottom: 0;
}

#icon {
  width: 80px;
  text-align: center;
  opacity: 30%;
  transition: opacity 0.3s;
}

#icon:hover {
  opacity: 100%;
}

.panes {
  position: relative;
}

.splitpanes__pane {
  justify-content: center;
  align-items: center;
  display: flex;
}

.splitpanes__pane span {
  font-family: Helvetica, Arial, sans-serif;
  color: #000;
  font-size: 5em;
}
</style>
