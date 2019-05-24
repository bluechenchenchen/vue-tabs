<docs>

</docs>
<script>
import TabNav from './tab-nav';
  export default {
    components: {
      TabNav
    },
    props: {
      activeName: String
    },
    data() {
      return {
        currentName: this.activeName,
      }
    },
    methods: {
      handleTabClick(ev, tabName) {
        this.currentName = tabName
        this.$emit('tab-click', tabName, ev)
      },
      calcPaneInstances() {
        console.log(this.$slots.default)
        if (this.$slots.default) {
          const panes = this.$slots.default.map(item => {
            return {
              label: item.data.attrs.label || item.componentOptions.propsData.label,
              name: item.data.attrs.name || item.componentOptions.propsData.name,
            }
          })
          this.panes = panes
        }
      },
    },
    render(h) {
      let { panes, currentName, handleTabClick } = this
      const navData = {
        props: {
          panes,
          currentName,
          onTabClick: handleTabClick,
        }
      }
      return (
        <div class="tabs-container tabs">
          <tab-nav { ...navData }></tab-nav>
          <div class="tabs-panels">
            {this.$slots.default}
          </div>
        </div>
      )
    },
    created () {
      this.calcPaneInstances()
    },
}
</script>

<style lang="scss" scoped>

</style>


