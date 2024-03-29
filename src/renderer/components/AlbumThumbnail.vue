<template>
  <div class="album-thumbnail">
    <button
      class="album-cover"
      @click="$router.push({ name: 'Album', params: { id: albumId } })"
      @mouseenter="hover = true"
      @mouseleave="hover = false"
    >
      <img :src="albumImage" class="album-cover__image" />
      <div class="album-cover__overlay" v-show="hover">
        <button class="album-cover-overlay__icon">
          <SvgIcon fill="white" :path="heartOutlinedPath" />
        </button>
        <button class="album-cover-overlay__icon--large-interactive">
          <SvgIcon fill="white" :path="playOutlinedPath" />
        </button>
        <button class="album-cover-overlay__icon">
          <SvgIcon fill="white" :path="navigationFilledPath" />
        </button>
      </div>
    </button>
    <span class="album-thumbnail__title truncate-text--ellipsis">{{
      albumName
    }}</span>
    <span class="album-thumbnail__artists truncate-text--ellipsis">{{
      artistName
    }}</span>
  </div>
</template>

<script>
import SvgIcon from "@/components/ui/SvgIcon";

import * as IconPath from "@/../constants/iconPaths";

export default {
  name: "AlbumThumbnail",
  components: { SvgIcon },
  data() {
    return {
      hover: false,
      heartOutlinedPath: IconPath.HEART_OUTLINED,
      navigationFilledPath: IconPath.NAVIGATION_FILLED,
      playOutlinedPath: IconPath.PLAY_OUTLINED
    };
  },
  props: {
    albumId: {
      type: Number,
      required: true
    },
    albumImage: String,
    albumName: String,
    artistName: String
  }
};
</script>

<style lang="scss">
.album-thumbnail {
  @include margin($bottom: 1.5rem, $left: 1rem);
  @include flex($col: true);
}

.album-cover {
  @include size($w: 100%);
  position: relative;

  &::after {
    @include square-size(100%);
    @include absolute($top: 0, $left: 0);
    content: "\A";
    background: rgba(0, 0, 0, 0.55);
    opacity: 0;
    transition: all 0.25s;
    transition-timing-function: ease;
  }

  &:hover::after {
    opacity: 1;
  }

  &:focus {
    outline: none;
  }

  &__image {
    @include square-size(100%);
  }

  &__overlay {
    @include square-size(100%);
    @include flex($row: true, $h-center: true, $v-center: true);
    @include absolute($top: 0, $left: 0);
    z-index: 10;
  }

  &-overlay__icon {
    @include square-size(1.5rem);
    fill: white;

    &--large-interactive {
      @include square-size(3rem);
      @include margin-axis($x: 1rem);
      fill: white;
      transition: all 0.05s;
      transition-timing-function: ease;

      &:hover {
        @include square-size(3.15rem);
        @include margin-axis($x: 0.925rem);
      }
    }
  }
}

.album-thumbnail__title {
  @include margin($top: 0.5rem);
  font-size: $text-xs;
  font-weight: 600;
}

.album-thumbnail__artists {
  font-size: $text-xs;
  color: $medium-emphasis;
}
</style>
