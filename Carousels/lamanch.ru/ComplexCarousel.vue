<template>
  <vue-tabs class="complex-carousel">
    <v-tab v-for="(tabItem, i) in complexData.navigation" :title="tabItem.title" :icon="tabItem.icon" :key="tabItem.title.concat(i)">
     <el-row>
       <el-col :span="18">
         <carousel
             class="complex-carousel_carousel"
             :per-page="1"
             pagination-active-color="#f0ad19"
             pagination-color="#fff"
             navigation-prev-label='<i class="fas fa-chevron-left"></i>'
             navigation-next-label='<i class="fas fa-chevron-right"></i>'
             :pagination-enabled="true"
             :navigation-enabled="true">
           <slide class="complex-carousel_carousel_slide" v-for="(slide, i) in tabItem.carousel" :key="slide.image.concat(i)">
             <img :src="slide.image" :alt="slide.alt">
           </slide>
         </carousel>
       </el-col>
       <el-col :span="6">
         <div class="complex-carousel_text">
           <vue-tabs class="complex-carousel_text_tabs">
             <v-tab :title="tabContent.tab"  v-for="(tabContent, i) in tabItem.content" :key="tabContent.title.concat(i)">
               <div class="complex-carousel_text_title">{{ tabContent.title }}</div>
               <div class="complex-carousel_text_content" v-html="tabContent.text"></div>
             </v-tab>
           </vue-tabs>
         </div>
       </el-col>
     </el-row>
    </v-tab>
  </vue-tabs>



</template>

<script>
export default {
  data() {
    return {
      complexData: {
        navigation: [
          {
            title: 'Гайд парк',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 2',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/news-modal-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/news-modal-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 3',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
          {
            title: 'Гайд парк 4',
            icon: 'tab-icon fab fa-angellist',
            carousel: [
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              },
              {
                image: 'assets/img/index/complex-slide-1.jpg',
                alt: ''
              }
            ],
            content: [
              {
                tab: 'Инфраструктура 1',
                title: 'Конно-спортивный клуб 1',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              },
              {
                tab: 'Инфраструктура 2',
                title: 'Конно-спортивный клуб 2',
                text: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.'
              }
            ]
          },
        ],
      }
    }
  }
}
</script>

<style lang="scss">
@import "../scss/utils/vars.scss";
.complex-carousel {
  display: flex;
  justify-content: space-between;
  height: 580px;
  max-height: 580px;

  &_carousel {
    flex: 1 1 auto;
  }
  &_carousel_slide {}
  &_text {
    width: 310px;
    max-width: 310px;
    padding: 21px 30px;

    &_title {
      font-size: 30px;
      font-weight: 300;
      line-height: 1.3;
      color: #000;
      margin-bottom: 24px;
    }
    &_content {
      overflow-y: auto;
      height: 314px;
      font-size: 14px;
    }
    &_tabs {
      .tab.active {
        background-color: transparent!important;
      }
      .tabs__link {
        padding: 0!important;
        font-size: 15px!important;
      }
      .tab-content {
        padding-top: 45px;
      }
    }
  }

  & > .nav-tabs-navigation .nav-tabs {
    background-color: $dark-gray-color;
    width: 150px;
    max-width: 150px;
    display: flex;
    align-items: stretch;
    flex-direction: column;
    color: #fff;
    padding: 0;
  }
  & > .tab-content {
    width: calc(1279px - 166px);
    max-width: calc(1279px - 166px);
    background-color: $gray-color;
    display: flex;
  }
  .tab.active {
    background-color: $primary-color;
    color: #fff;
  }
  .tabs__link {
    position: relative;
    font-size: 11px;
    margin: 0;
    padding: 40px 10px 10px;
    display: block;
    text-align: center;
  }
  & > .nav-tabs-navigation {
    padding-right: 16px;
    overflow-y: auto;
    overflow-x: hidden;
    height: 100%;
    border-bottom: 0;
  }
  .tab-icon {
    position: absolute;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 27px;
  }
  & > .nav-tabs-navigation .active_tab.tabs__link {
    border-bottom: 0;
    color: #fff;
  }
  .VueCarousel-navigation-prev {
    z-index: 10;
    left: -200px;
    @media screen and (max-width: 1400px) {
      left: -135px;
    }
  }
  .VueCarousel-navigation-next {
    z-index: 10;
    right: -350px;
    @media screen and (max-width: 1400px) {
      right: -280px;
    }
  }
  .VueCarousel-pagination {
    position: absolute;
    top: unset;
    bottom: 60px;
  }
  .VueCarousel-dot {
    border-radius: 0;
  }
  .VueCarousel-inner {
    flex-basis: 100%!important;
    /*width: 100%!important;*/
    /*height: 600px!important;*/
  }
  .VueCarousel-slide > img {
    height: 580px;
    max-height: 580px;
  }
}
</style>
