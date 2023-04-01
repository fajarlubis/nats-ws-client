<template>
  <Tutorial />
</template>

<script>
import {
  connect,
  StringCodec,
} from "nats.ws/cjs/nats";

export default {
  name: 'IndexPage',
  async fetch() {
    const sc = StringCodec();
    const nc = await connect({ servers: ["ws://10.104.0.15:32244"] });

    nc.subscribe("pid.notification", {
      callback: (err, msg) => {
        console.log(`${sc.decode(msg.data)}`);
      },
    });
  }
}
</script>
