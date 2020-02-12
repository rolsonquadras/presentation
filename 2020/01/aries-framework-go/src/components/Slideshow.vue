<template lang='pug'>
#Slideshow.eg-theme-agrume
  .eg-slideshow
    slide
      h3 Edge Agent Routing Topology
        mermaid.
          graph TB;
          A1(Agent One) -->|HTTP| R(Mediator);
          R -->|WS| A(Agent Two);
    <DemoSetup :routerURL=routerAgentURL :agentURL=humanAgentURL role="" :lobbyURL=lobbyServerURL />
    <DemoSetup :routerURL=routerAgentURL :agentURL=botAgentURL role=" (bot)" v-if="this.showBotSetup" :lobbyURL=lobbyServerURL />
    <DemoMultiUser :botAgentURL=botAgentURL :humanAgentURL=humanAgentURL :humanAgentWebhookURL=humanAgentWebhookURL :autoBotMsgRegister=autoBotMsgRegister :lobbyURL=lobbyServerURL />
</template>

<script>
import { Slideshow } from 'eagle.js'
import mermaid from './mermaid.vue'
import DemoSetup from './DemoSetup.vue'
import DemoBasicMessage from './DemoBasicMessage.vue'
import DemoMultiUser from './DemoMultiUser.vue'

export default {
  name: 'Slideshow',
  props: {
    routerAgentURL: { default: process.env.VUE_APP_ROUTER_AGENT_URL },
    humanAgentURL: { default: process.env.VUE_APP_HUMAN_AGENT_URL },
    humanAgentWebhookURL: { default: process.env.VUE_APP_HUMAN_AGENT_WEBHOOK_URL },
    botAgentURL: { default: process.env.VUE_APP_BOT_AGENT_URL },
    showBotSetup: { default: process.env.VUE_APP_SHOW_BOT_SETUP != 'false' },
    autoBotMsgRegister: { default: process.env.VUE_APP_AUTO_BOT_MSG_REGISTER != 'false' },
    lobbyServerURL: { default: process.env.VUE_APP_LOBBY_URL },
  },
  mixins: [ Slideshow ],
  components: {
    mermaid,
    DemoSetup,
    DemoMultiUser,
    DemoBasicMessage
  }
}
</script>
