<template>
  <div class="home">
    <Card :title="$t('home.title')" bordered>
      <Space class="items">
        <div class="item">
          <span class="key">{{ $t('home.total_fee') }}</span>
          <span class="value">{{ parseFloat(my_info.total_fee || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.month_fee') }}</span>
          <span class="value">{{ parseFloat(my_info.month_fee || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.month_quota') }}</span>
          <span class="value">{{ parseFloat(my_info.month_quota || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.balance') }}</span>
          <span class="value">{{ parseFloat(my_info.balance || 0) }}<span class="sub">USD</span></span>
        </div>
      </Space>
    </Card>

    <Card :title="$t('home.all')" bordered v-if="false">
      <Space class="items">
        <div class="item">
          <span class="key">{{ $t('home.total_fee') }}</span>
          <span class="value">{{ parseFloat(my_info.total_fee || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.month_fee') }}</span>
          <span class="value">{{ parseFloat(my_info.month_fee || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.month_quota') }}</span>
          <span class="value">{{ parseFloat(my_info.month_quota || 0) }}<span class="sub">USD</span></span>
        </div>
        <div class="item">
          <span class="key">{{ $t('home.balance') }}</span>
          <span class="value">{{ parseFloat(my_info.balance || 0) }}<span class="sub">USD</span></span>
        </div>
      </Space>
    </Card>
  </div>
</template>
<script>
export default {
  data() {
    return {
      loading: false,
      my_info: {},
    }
  },
  computed: {
    is_admin() {
      return localStorage.getItem('role') == 'admin'
    }
  },
  created() {
    const host = localStorage.getItem("host");
    const key = localStorage.getItem("key");
    localStorage.setItem("host", host);
    this.$http.get(host + '/user/api-key/mine', null, key).then(res => {
      if (res.success) {
        this.my_info = res.data;
      } else {
        alert(res.data);
      }
    }).finally(() => {
      this.loading = false
    });
  },
  methods: {

  }
}
</script>
<style lang="less">
.home {
  padding: 20px;

  .items {
    width: 100%;
  }

  .item {
    background: var(--kui-color-gray-90);
    border-radius: 16px;
    flex: 1;
    padding: 20px;
    display: flex;
    flex-direction: column;

    .key {
      font-weight: bold;
      margin-right: 10px;
    }

    .value {
      margin-top: 8px;
    }

    .sub {
      color: var(--kui-color-gray-30);
      font-size: 12px;
      margin-left: 8px;
    }


  }

  .k-card {
    margin-bottom: 20px;
  }

 
}
</style>