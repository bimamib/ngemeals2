<template>
  <div>
    <header
      class="flex items-center justify-between h-16 px-4 bg-white border shadow"
    >
      <!-- Mobile hamburger menu -->
      <button
        class="block p-2 rounded-lg md:hidden hover:bg-gray-100"
        @click="isMenuOpen = !isMenuOpen"
        aria-label="Menu"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="w-6 h-6 text-gray-600"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            strokeWidth="2"
            d="M4 6h16M4 12h16M4 18h16"
          />
        </svg>
      </button>

      <!-- Navigation container -->
      <div class="navigation-container" :class="{ 'mobile-open': isMenuOpen }">
        <div class="wrap">
          <router-link
            :to="{ name: 'home' }"
            class="label"
            :class="{ active: $route.name === 'home' }"
            @click="isMenuOpen = false"
          >
            <span>Home</span>
          </router-link>

          <router-link
            :to="{ name: 'byName' }"
            class="label"
            :class="{ active: $route.name === 'byName' }"
            @click="isMenuOpen = false"
          >
            <span>Search Meals</span>
          </router-link>

          <router-link
            :to="{ name: 'byLetter' }"
            class="label"
            :class="{ active: $route.name === 'byLetter' }"
            @click="isMenuOpen = false"
          >
            <span>Meals By Letter</span>
          </router-link>

          <router-link
            :to="{ name: 'ingredients' }"
            class="label"
            :class="{ active: $route.name === 'ingredients' }"
            @click="isMenuOpen = false"
          >
            <span>Meals By Ingredient</span>
          </router-link>

          <div class="bar"></div>
          <div class="slidebar"></div>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
    };
  },
  watch: {
    $route() {
      this.isMenuOpen = false;
    },
  },
};
</script>

<style scoped>
.navigation-container {
  display: flex;
  justify-content: center;
  width: 100%;
}

.wrap {
  --round: 10px;
  --p-x: 8px;
  --p-y: 4px;
  --w-label: 175px;
  display: flex;
  align-items: center;
  padding: var(--p-y) var(--p-x);
  position: relative;
  background: #f0f0f0;
  border-radius: var(--round);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.label {
  cursor: pointer;
  outline: none;
  font-size: 0.875rem;
  letter-spacing: initial;
  font-weight: 500;
  color: #333;
  background: transparent;
  padding: 12px 16px;
  width: var(--w-label);
  min-width: var(--w-label);
  text-decoration: none;
  user-select: none;
  transition: color 0.25s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 2;
  text-align: center;
}

.label.active {
  color: #fff;
}

.bar {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  position: absolute;
  transform-origin: 0 0 0;
  height: 100%;
  width: var(--w-label);
  z-index: 0;
  transition: transform 0.5s cubic-bezier(0.33, 0.83, 0.99, 0.98);
}

.bar::before,
.bar::after {
  content: "";
  position: absolute;
  height: 4px;
  width: 100%;
  background: #333;
}

.bar::before {
  top: 0;
  border-radius: 0 0 9999px 9999px;
}

.bar::after {
  bottom: 0;
  border-radius: 9999px 9999px 0 0;
}

.slidebar {
  position: absolute;
  height: calc(100% - (var(--p-y) * 4));
  width: var(--w-label);
  border-radius: calc(var(--round) - var(--p-y));
  background: #666;
  transform-origin: 0 0 0;
  z-index: 0;
  transition: transform 0.5s cubic-bezier(0.33, 0.83, 0.99, 0.98);
}

/* Positioning the active bar and slidebar */
.label:nth-child(1).active ~ .bar,
.label:nth-child(1).active ~ .slidebar {
  transform: translateX(0) scaleX(1);
}

.label:nth-child(2).active ~ .bar,
.label:nth-child(2).active ~ .slidebar {
  transform: translateX(100%) scaleX(1);
}

.label:nth-child(3).active ~ .bar,
.label:nth-child(3).active ~ .slidebar {
  transform: translateX(200%) scaleX(1);
}

.label:nth-child(4).active ~ .bar,
.label:nth-child(4).active ~ .slidebar {
  transform: translateX(300%) scaleX(1);
}

/* Responsive styles */
@media (max-width: 768px) {
  .navigation-container {
    position: fixed;
    top: 4rem;
    left: 0;
    right: 0;
    background: white;
    transform: translateY(-150%);
    transition: transform 0.3s ease-in-out;
    z-index: 50;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .navigation-container.mobile-open {
    transform: translateY(0);
  }

  .wrap {
    flex-direction: column;
    width: 100%;
    border-radius: 0;
    padding: 1rem 0;
    box-shadow: none;
    background: white;
  }

  .label {
    width: 100%;
    min-width: 100%;
    padding: 1rem;
  }

  .bar,
  .slidebar {
    display: none;
  }

  .label.active {
    background: #666;
    margin: 0.25rem 1rem;
    border-radius: var(--round);
    width: calc(100% - 2rem);
    min-width: calc(100% - 2rem);
  }
}

/* Larger screens */
@media (min-width: 769px) {
  .wrap {
    --w-label: 165px;
  }
}

@media (min-width: 1024px) {
  .wrap {
    --w-label: 175px;
  }
}
</style>
