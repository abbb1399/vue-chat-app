<template>
  <div class="home">
    <ChatWindow
      height="calc(100vh - 20px)"
			:current-user-id="currentUserId"
			:rooms="rooms"
			:rooms-loaded="true"
			:messages="messages"
			:messages-loaded="messagesLoaded"
			@send-message="sendMessage"
			@fetch-messages="fetchMessages"
			@delete-message="deleteMsg"
    />
  </div>
</template>

<script>
// @ is an alias to /src

import ChatWindow from './ChatWindow.vue'
// import 'vue-advanced-chat/dist/vue-advanced-chat.css'

export default {
  name: 'Home',
  components: {
    ChatWindow
  },
  data() {
		return {
			currentUserId: 1234,
			rooms: [
				{
					roomId: 1,
					roomName: 'Room 1',
					avatar: 'https://66.media.tumblr.com/avatar_c6a8eae4303e_512.pnj',
					users: [
						{ _id: 1234, username: 'John Doe' },
						{ _id: 4321, username: 'John Snow' },
						{ _id: 5678, username: 'Paul Jeon' }
					]
				}
			],
			messages: [],
			messagesLoaded: false,
		}
	},
  methods: {
		fetchMessages({ options = {} }) {
			// console.log(options)
			
			setTimeout(() => {
				// 방이 처음 열렸을때 reset:true
				if (options.reset) {
					this.messages = this.addMessages(true)
				} else {
					this.messages = [...this.addMessages(), ...this.messages]
					this.messagesLoaded = true
				}
				// this.addNewMessage()
			})
		},

		addMessages(reset) {
			// console.log(reset)
			const messages = []

			for (let i = 0; i < 10; i++) {
				messages.push({
					_id: reset ? i : this.messages.length + i,
					content: `${reset ? '' : 'paginated'} message ${i + 1}`,
					senderId: 4321,
					username: 'John Doe',
					date: '13 November',
					timestamp: '10:20'
				})
			}

			return messages
		},

		sendMessage(message) {
			console.log(message)
			this.messages = [
				...this.messages,
				{
					_id: this.messages.length,
					content: message.content,
					senderId: this.currentUserId,
					timestamp: new Date().toString().substring(16, 21),
					date: new Date().toDateString()
				}
			]
		},

		// addNewMessage() {
		// 	setTimeout(() => {
		// 		this.messages = [
		// 			...this.messages,
		// 			{
		// 				_id: this.messages.length,
		// 				content: 'NEW MESSAGE',
		// 				senderId: 4321,
		// 				timestamp: new Date().toString().substring(16, 21),
		// 				date: new Date().toDateString()
		// 			}
		// 		]
		// 	}, 2000)
		// },
		deleteMsg (message) {
      console.log(message)
      const aa = document.querySelectorAll('.vac-message-card')
      console.log(aa)

      // console.log(roomId)
      // console.log(message)
      // const aa = this.messages.filter(v => v._id !== message._id)
      // this.messages = aa
    },



	}


}
</script>



<style lang="scss">
body {
	font-family: 'Quicksand', sans-serif;
}
</style>
