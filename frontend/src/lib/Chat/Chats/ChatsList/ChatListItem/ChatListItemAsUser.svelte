<script lang="ts">
  import ChatListItem from "./ChatListItem.svelte";
  import type { Socket } from 'socket.io-client'
  import { app, user } from '../../../../../stores'


  export let socket: Socket,
  name: string,
  socketId: string

  function clickHandler() {
    if ($app.search.mode)
      socket.emit('create chat', { name: '', users: [$user, { username: name, socketId: socketId }] })
    else
      throw new Error('Put ChatListItemAsUser in chats without search mode')
  }
</script>

<ChatListItem name={name} on:click={clickHandler} />
