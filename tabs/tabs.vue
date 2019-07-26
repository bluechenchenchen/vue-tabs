<docs>

</docs>
<script>
import TabNav from "./tab-nav";
export default {
  components: { TabNav },
  props: { activeName: String },
  data() {
    return { currentName: this.activeName, panes: [] };
  },
  methods: {
    handleTabClick(ev, tabName) {
      this.currentName = tabName;
      this.$emit("tab-click", tabName, ev);
    },
    calcPaneInstances() {
      if (this.$slots.default) {
        const paneSlots = this.$slots.default.filter(
          vnode =>
            vnode.tag &&
            vnode.componentOptions &&
            vnode.componentOptions.Ctor.options.name === "TabPane"
        );
        const panes = paneSlots.map(
          ({ componentInstance }) => componentInstance
        );
        const panesChanged = !(
          panes.length === this.panes.length &&
          panes.every((pane, index) => pane === this.panes[index])
        );
        if (panesChanged) {
          this.panes = panes;
        }
        // this.panes = panes;
      } else if (this.panes.length !== 0) {
        this.panes = [];
      }
    }
  },
  render() {
    let { panes, currentName, handleTabClick } = this;
    const navData = {
      props: {
        panes,
        currentName,
        onTabClick: handleTabClick
      }
    };
    return (
      <div class="tabs-container tabs">
        <tab-nav {...navData} />
        <div class="tabs-panels">{this.$slots.default}</div>
      </div>
    );
  },
  created() {
    // this.$on("tab-nav-update", this.calcPaneInstances.bind(null, true));
  },
  mounted() {
    this.calcPaneInstances();
  },

  updated() {
    this.calcPaneInstances();
    // eslint-disable-next-line no-console
    // console.log("updated")
  }
};
</script>

<style lang="scss" scoped></style>
