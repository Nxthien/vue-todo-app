<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div v-show='message.length > 0'>
      {{ message }}
    </div>
    <div class='ui centered card' v-show="isCreating">
      <div class='content'>
        <div class='ui form'>
          <div class='field'>
            <label>Title</label>
            <input v-model="titleText" type='text' ref='title' defaultValue="">
          </div>
          <div class='field'>
            <label>Project</label>
            <input type='text' ref='project' defaultValue="" v-model='projectText'>
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="sendForm()">
              Create
            </button>
            <button class='ui basic red button' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
	export default {
		data() {
			return {
				titleText: '',
				projectText: '',
				isCreating: false,
        message: ''
			}
		},
		methods: {
			closeForm() {
				this.isCreating = false;
			},
			openForm() {
				this.isCreating = true;
			},
			sendForm() {
        if (this.titleText.length > 0 && this.projectText.length > 0) {
          const title = this.titleText;
          const project = this.projectText;

          this.$emit('create-todo', {
              title,
              project,
              done: false
            }
          ),
          this.isCreating = false;
        } else {
          this.message = 'Create todo failed'
        }
			}
 
		}
	}
</script>