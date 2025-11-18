<script setup lang="ts">
import { useRouter, withBase } from "vitepress";

type Props = {
  prev?: {
    path: string;
    title: string;
  };
  next?: {
    path: string;
    title: string;
  };
};

const { prev, next } = defineProps<Props>();
const router = useRouter();

function goToLink(path?: string) {
  if (path) {
    router.go(withBase(path));
  }
}
</script>

<template>
  <div>
    <hr />

    <div class="prev-next-container">
      <div v-show="prev" class="prev-next-btn" @click="goToLink(prev?.path)">
        <div class="prev-next-label">Previous post</div>
        <div>{{ prev?.title }}</div>
      </div>
      <div
        v-show="next"
        class="prev-next-btn next-btn"
        @click="goToLink(next?.path)"
      >
        <div class="prev-next-label">Next post</div>
        <div>{{ next?.title }}</div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.prev-next-container {
  display: flex;
  justify-content: space-between;
  font-size: 0.85rem;

  .prev-next-btn {
    display: flex;
    flex-direction: column;
    background-color: var(--vp-c-bg-soft);
    border-radius: 1rem;
    border: 1px solid var(--vp-c-bg-soft);
    padding: 1rem;
    margin-top: 0.25rem;
    cursor: pointer;

    &:hover {
      border-color: var(--vp-c-brand-1);
    }

    &.next-btn {
      margin-left: auto;
      align-items: flex-end;
    }

    .prev-next-label {
      color: var(--vp-c-text-2);
    }
  }
}
</style>
