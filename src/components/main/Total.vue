<template>
  <div>
    <div class="tables-top">
      <span class="tl-table-tit">{{ $t("main.tl.name") }}</span>
      <div class="tl-table-line"></div>
    </div>

    <div class="row tl-total-info">
      <div class="col-xs-12 col-sm-12 col-md-6 col-lg-3 col-xl-3">
        {{ $t("main.tl.total.name") }}
        <span class="total-count">{{
          $HelperTools.toFinancialVal(totals.Total) || 0
        }}</span>
      </div>
      <div class="col-xs-12 col-sm-12 col-md-6 col-lg-3 col-xl-3">
        {{ $t("main.tl.total.activeU") }}
        <span class="total-count">{{
          $HelperTools.toFinancialVal(totals.DayActiveAddressCount) || 0
        }}</span>
      </div>
      <div class="col-xs-12 col-sm-12 col-md-6 col-lg-3 col-xl-3">
        {{ $t("main.tl.total.txn") }}
        <span class="total-count">{{
          $HelperTools.toFinancialVal(totals.DayTxCount) || 0
        }}</span>
      </div>
      <div class="col-xs-12 col-sm-12 col-md-6 col-lg-3 col-xl-3">
        {{ $t("main.tl.total.volume") }}
        <span class="total-count">{{
          (totals.DayOng
            ? $HelperTools.toFinancialVal(parseFloat(totals.DayOng).toFixed(2))
            : 0) +
            " ONG, " +
            (totals.DayOnt || 0) +
            " ONT"
        }}</span>
      </div>
    </div>

    <div class="tl-total-info-line"></div>
  </div>
</template>

<script>
export default {
  created() {
    this.$store.dispatch("getDAppTotals").then();
  },
  computed: {
    totals() {
      return this.$store.getters.dAppTotals || {};
    }
  }
};
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.tables-top {
  margin-top: 14px;
}
.tl-table-tit {
  font-size: 16px;
  color: rgba(70, 159, 219, 1);
}
.tl-total-info {
  margin: 30px -15px 30px !important;

  div {
    font-size: 14px;
    color: rgba(74, 74, 74, 1);
  }
  .total-count {
    color: rgba(70, 159, 219, 1);
  }
}
.tl-total-info-line {
  background-color: #e0e0e0;
  height: 1px;
}
</style>
