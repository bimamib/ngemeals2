<template>
  <div>
    <header
      class="flex items-center justify-between h-20 bg-white border shadow"
    >
      <div class="navigation-container">
        <div class="wrap">
          <router-link
            :to="{ name: 'home' }"
            class="label"
            :class="{ active: $route.name === 'home' }"
          >
            <span>Home</span>
          </router-link>

          <router-link
            :to="{ name: 'byName' }"
            class="label"
            :class="{ active: $route.name === 'byName' }"
          >
            <span>Search Meals</span>
          </router-link>

          <router-link
            :to="{ name: 'byLetter' }"
            class="label"
            :class="{ active: $route.name === 'byLetter' }"
          >
            <span>Meals By Letter</span>
          </router-link>

          <router-link
            :to="{ name: 'ingredients' }"
            class="label"
            :class="{ active: $route.name === 'ingredients' }"
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
  name: "MealAppLayout",
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
  --w-label: 120px;
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
</style>
