<script setup>
import { ref, computed } from 'vue'
import Dashboard from './components/Dashboard.vue'
import { assets, categories } from './data/assetData.js'
import './assets/app.css';

const assetData = ref({
  assets: assets,
  categories: categories,
  departments: computed(() => [...new Set(assets.map(asset => asset.department))]),
  statusOptions: ['In Use', 'Storage', 'Under Repair', 'Disposal'],
  totalValue: computed(() => assets.reduce((sum, asset) => sum + asset.value, 0)),
  assetCount: computed(() => assets.length)
})

const updateAsset = (updatedAsset) => {
  const index = assetData.value.assets.findIndex(a => a.assetID === updatedAsset.assetID)
  if (index !== -1) assetData.value.assets[index] = updatedAsset
}
</script>

<template>
  <el-container class="app-container">
    <!-- HEADER -->
    <el-header height="60px" class="app-header">
      <div class="header-content">
        <div class="logo-section">
          <img 
            src="/images/companyLogo.png" 
            class="logo"
            alt="Company Logo"
          >
        </div>
        <h1 class="title">DIGITAL ASSET MANAGEMENT SYSTEM</h1>
      </div>
    </el-header>

    <!-- MAIN CONTENT -->
    <el-main class="app-main">
      <Dashboard 
        :assetData="assetData" 
        @update-asset="updateAsset"
      />
    </el-main>
  </el-container>
</template>



