<template>
<div class="tabBar">
    <div v-for="tab in tabs" :key="tab" class="tab">
        {{tab}}
    </div>
</div>
<div id="terminal" ref="terminal" class="cmd"></div>  
</template>

<script>

import { Terminal } from "xterm"
import "xterm/css/xterm.css"
import "xterm/lib/xterm.js"

export default {
    name: 'console',
    setup () {

    },
    data () {
        return {
            tabs: []
        }
    },
    mounted () {
        let term = new Terminal({
            rendererType: "canvas",
            rows: 100,
            cols: 100,
            convertEol: true,
            disableStdin: false,
            cursorStyle: "underline",
            cursorBlink: true,
            theme: {
                foreground: '#7e9192',
                background: '#002833',
                cursor: "help",
                lineHeight: 16
            }
        })

        term.open(this.$refs["terminal"])
        
        term.prompt = () => {
            term.write("\r\n$ ");
        }
        term.prompt()

        term.onKey(e => {
            term.write(e.key)
            if (e.key == '\r') {
                term.write('\n')
            }
        })
    }
}

</script>

<style scoped>
.cmd {
    
}
.tabBar {

}
.tab { 

}
</style>