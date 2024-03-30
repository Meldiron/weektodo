<template>
  <div class="modal fade" id="DeviceIdModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Set Device ID</h5>
          <i id="device-modal-close" class="bi-x close-modal" data-bs-dismiss="modal"></i>
        </div>
        <div class="modal-body">
          <label class="form-label">Device ID:</label>
          <input class="col-sm-9 form-select" v-model="deviceId" />

          <button
            @click="onSaveDeviceId"
            id="clear-data-btn"
            type="button"
            class="btn py-1 mt-2 px-2 border"
            style="width: 140px"
          >
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DeviceIdModal",
  data() {
    let deviceId = localStorage.getItem('deviceId');

    if(!deviceId) {
      deviceId = 'd_' + Date.now();
      localStorage.setItem('deviceId', deviceId);
    }
    
   return {
     deviceId: deviceId
   };
  },
  methods: {
    onSaveDeviceId() {
      localStorage.setItem('deviceId', this.deviceId);
      document.getElementById('device-modal-close').click();
      window.location.reload();
    }
  },
  computed: {},
};
</script>

<style scoped lang="scss">
@import "/src/assets/style/globalVars.scss";

.modal-dialog {
  max-width: 370px;
}

.modal-body {
  height: 380px;
  overflow: auto;
  margin-bottom: 20px;
}

.table {
  --bs-table-hover-bg: #f4f4f4;
  color: #212529;
}

.dark-theme .table {
  --bs-table-bg: #21262d;
  --bs-table-striped-bg: #2c3034;
  --bs-table-striped-color: #fff;
  --bs-table-active-bg: #373b3e;
  --bs-table-active-color: #fff;
  --bs-table-hover-bg: #323539;
  --bs-table-hover-color: #fff;
  color: #fff;
  border-color: #373b3e;
}

.grip-horizontal {
  cursor: grabbing;

  &:hover {
    color: black;
  }

  .dark-theme & {
    color: #babbbe;

    &:hover {
      color: white;
    }
  }
}

.custom-lists {
  list-style: none;
  padding: 0px 10px 10px 10px;
  margin-top: 10px;
  max-height: 320px;
  overflow-y: auto;

  li > div {
    -webkit-user-drag: element;
  }

  .custom-list {
    border-bottom: 1px solid #eaecef;

    .dark-theme & {
      border-bottom: 1px solid #464647;
    }

    label {
      width: 100%;
      padding: 10px 5px 10px 0px;
      min-height: 38px;
      height: auto;

      * {
        pointer-events: none;
      }
    }

    .form-check-input {
      width: 16px !important;
      height: 16px !important;
      min-width: 16px;
      min-height: 16px;
    }

    i {
      color: #87888a;
      display: none;
      cursor: pointer;

      &:hover {
        color: black;
      }

      .checked & {
        opacity: 1 !important;
      }

      .dark-theme & {
        color: #babbbe;

        &:hover {
          color: white;
        }
      }
    }

    .drag-hover {
      color: rgba(157, 157, 157, 0.43);
      background-color: rgb(250, 249, 249);

      .dark-theme & {
        color: rgb(87, 87, 87);
        background-color: #1f1e20;
      }
    }

    &:hover {
      background-color: $btn-hover-bg-color;

      .dark-theme & {
        background-color: $dt-btn-hover-bg-color;
      }

      i {
        display: block;
      }
    }
  }
}
</style>
