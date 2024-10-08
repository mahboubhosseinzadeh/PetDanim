<template>
  <article v-if="posts.length != 0">
    <div
      v-for="(post, index) in posts.slice(1, 3)"
      :key="index"
      class="relative flex group mb-3 flex-row items-center p-4 rounded-3xl sm:bg-white sm:dark:!bg-dark-800 border border-neutral-200 dark:!border-dark-700/20 h-auto"
    >
      <nuxt-link class="absolute inset-0 z-0" :to="`/${post.slug}`"></nuxt-link>
      <div class="flex flex-col flex-grow">
        <div class="space-y-3 mb-4">
          <PostCategory status="danger" :text="post.category.title" />
          <h2
            class="block font-semibold text-sm sm:text-base dark:!text-dark-700"
          >
            <nuxt-link
              class="line-clamp-2 dark:!text-gray-300"
              title="360-degree video: How Microsoft deployed a datacenter to the bottom of the ocean"
              :to="`/${post.slug}`"
              >{{ post.title }}
            </nuxt-link>
          </h2>
          <div
            class="nc-PostCardMeta inline-flex items-center flex-wrap text-neutral-800 dark:text-neutral-200 leading-none text-xs"
          >
            <Author>
              <AuthorImage :authorImage="post.author.profile == null ? '/2.webp' : post.author.profile" />
              <AuthorName :authorname="`${post.author.name} ${post.author.family}`" />
            </Author>
            <span
              class="text-neutral-500 dark:!text-dark-700 mx-[6px] font-medium"
              >·</span
            >
            <Data :date="post.created_at" />
          </div>
        </div>
        <div class="flex items-center flex-wrap justify-between mt-auto">
          <div class="flex items-center space-x-2 rtl:space-x-reverse relative">
            <LikeButton @click="doLikePost(post)" :count="post.likes.length" :isRed="authUser != null ? authUser.likes.some(item => item.favoritable_id === post.id && item.favoritable_type === 'App\\Models\\AdminPost') : false" />
            <CommentButton :count="post.comments.length" />
          </div>
          <div
            class="flex items-center space-x-2 text-xs text-neutral-700 dark:!text-neutral-300 relative"
          >
            <BookmarkButton @click="doBookmarkPost(post)" :isFill="authUser != null ? authUser.bookmarks.some(item => item.bookmarkable_id === post.id && item.bookmarkable_type === 'App\\Models\\AdminPost') : false" />
          </div>
        </div>
      </div>
      <nuxt-link
        class="block relative flex-shrink-0 w-24 h-24 sm:w-40 sm:h-full ms-3 sm:ms-5 rounded-2xl overflow-hidden z-0"
        :to="`/${post.slug}`"
        ><img
          :alt="post.title"
          class="object-cover w-full h-[120px]"
          :src="`${appBaseUrl}/storage/${post.image}`" /><span class="absolute bottom-1 start-1"
          ><div class="nc-PostTypeFeaturedIcon"></div></span
      ></nuxt-link>
    </div>
  </article>
</template>

<script setup>
import PostCategory from "~/components/TemplateParts/Badge/index.vue";
import Author from "@/components/TemplateParts/MetaAction/Author/Author.vue";
import AuthorName from "@/components/TemplateParts/MetaAction/Author/AuthorName.vue";
import AuthorImage from "@/components/TemplateParts/MetaAction/Author/AuthorImage.vue";
import LikeButton from "@/components/TemplateParts/MetaAction/Like.vue";
import CommentButton from "@/components/TemplateParts/MetaAction/Comment.vue";
import BookmarkButton from "@/components/TemplateParts/MetaAction/Bookmark.vue";
import Data from "@/components/TemplateParts/MetaAction/Data.vue";

import {usePetdanimStore} from '@/store/petdanimStore'
import {storeToRefs} from 'pinia'

const {$toast} = useNuxtApp()

const petdanimStore = usePetdanimStore()
const {authUser} = storeToRefs(petdanimStore)


const {appBaseUrl} = useRuntimeConfig().public
const props = defineProps({
  posts: {
    required: true,
    type: [Array, Object],
  },
});


const doLikePost = async (post) => {
  if(authUser.value != null) {
    const result = await petdanimStore.doLikePost({
      post_id: post.id,
      type: "admin"
    })
    if(result.status == 200) {
      post.likes = result.result.post_likes
      authUser.value.likes = result.result.user_likes
    }
  } else {
    $toast("جهت پسندیدن این پست ابتدا باید وارد حساب کاربری خود شوید" , {
      "theme": "colored",
      "type": "error"
    });
  }
}

const doBookmarkPost = async (post) => {
  if(authUser.value != null) {
    const result = await petdanimStore.doBookmarkPost({
      post_id: post.id,
      type: "admin"
    })
    if(result.status == 200) {
      post.bookmarks = result.result.post_bookmarks
      authUser.value.bookmarks = result.result.user_bookmarks
    }
  } else {
    $toast("جهت افزودن این پست به ذخیره ها ابتدا باید وارد حساب کاربری خود شوید" , {
      "theme": "colored",
      "type": "error"
    });
  }
}
</script>
