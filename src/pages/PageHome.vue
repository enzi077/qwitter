<template>
  <q-page class="realtive-postion">
    <q-scroll-area class="absolute full-width full-height">
    <div class="q-py-lg q-px-md row q-col-gutter-md items-end">
        <div class="col">
            <q-input
                bottom-slots
                v-model="newQweetContent"
                placeholder="What's happening?"
                counter
                maxlength="280"
                autogrow
                class="new-qweet"
            >
                <template v-slot:before>
                    <q-avatar size="xl">
                        <img src="https://cdn.quasar.dev/img/avatar5.jpg">
                    </q-avatar>
                </template>
            </q-input>
        </div>
        <div class="col col-shrink">
            <q-btn
                :disabled="!newQweetContent"
                unelevated
                rounded
                color="primary"
                label="Qweet"
                no-caps
                class="q-mb-lg"
                @click="addNewQweet"
            />
        </div>
    </div>
    
    <q-separator
      size="10px"
      color="grey-2"
      class="divider"
    />
    
    <q-list separator>
        <transition-group
            appear
            enter-active-class="animated fadeIn slow"
            leave-active-class="animated fadeOut slow"
        >
            <q-item 
                class="q-py-md"
                v-for="qweet in qweets"
                :key="qweet.date"
            >
            <q-item-section avatar top>
            <q-avatar size="xl">
                <img src="https://cdn.quasar.dev/img/avatar5.jpg">
            </q-avatar>
            </q-item-section>

            <q-item-section>
            <q-item-label class="text-subtitle1">
                <strong>Janet</strong>
                <span class="text-grey">
                    @janet
                    <br class="lt-sm">&bull; {{ qweet.date }}
                </span>
            </q-item-label>
            <q-item-label class="qweet-content text-body1">
                {{qweet.content}}
            </q-item-label>
            <div class="row justify-between q-mt-sm qweet-icons">
                <q-btn
                    flat
                    round
                    size="sm"
                    color="grey"
                    icon="far fa-comment"
                    />
                    <q-btn
                    flat
                    round
                    size="sm"
                    color="grey"
                    icon="fas fa-retweet"
                    />
                    <q-btn
                    flat
                    round
                    size="sm"
                    color="grey"
                    icon="far fa-heart"
                    />
                    <q-btn
                    flat
                    round
                    size="sm"
                    color="grey"
                    icon="fas fa-trash"
                    @click="deleteQweet(qweet)"
                    />
            </div>
            </q-item-section>

            </q-item>
        </transition-group>
    </q-list>
    </q-scroll-area>
  </q-page>
</template>

<script>

export default {
  name: 'PageHome',
  data() {
      return {
        newQweetContent: '',
        qweets: [
            {
                content: 'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Atque officiis numquam voluptate unde, eius eum nostrum voluptas quis eligendi aperiam totam ipsa nobis ratione? Sint totam id officiis vero aperiam.',
                date: new Date(Date.now()).toUTCString()
            }
        ]
      }
  },
  methods:{
      addNewQweet() {
          let newQweet= {
              content: this.newQweetContent,
              date: new Date(Date.now()).toUTCString()
          }
          this.qweets.unshift(newQweet)
            this.newQweetContent=''
      },
      deleteQweet(qweet) {
          //DesqHCbKx05NK3TqO2US
          let dateToDelete=qweet.date
          let index=this.qweets.findIndex(qweet=> qweet.date === dateToDelete)
          this.qweets.splice(index,1)
      }
  },
}
</script>

<style lang="sass">
.new-qweet
    textarea
        font-size: 19px
        line-height: 1.4 !important
.divider
    border-top:1px solid
    border-bottom: 1px solid
    border-color: $grey-4
.qweet-content
    white-space: pre-line
.qweet-icons
    margin-left: -5px
</style>

