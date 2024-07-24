<script>
export default {
	data() {
		return {
			showModal: false,
		};
	},
	methods: {
		toggleModal() {
			this.showModal = !this.showModal;
		},
		beforeEnter(el) {
			console.log("Before Enter");
			el.style.opacity = 0;
		},
		enter(el, done) {
			console.log("Entering");
			setTimeout(() => {
				el.style.transition = "opacity 1s";
				el.style.opacity = 1;
				done();
			}, 0);
		},
		afterEnter(el) {
			console.log("After Enter");
		},
		enterCancelled(el) {
			console.log("Enter Cancelled");
		},
		beforeLeave(el) {
			console.log("Before Leave");
			el.style.opacity = 1;
		},
		leave(el, done) {
			console.log("Leaving");
			setTimeout(() => {
				el.style.transition = "opacity 1s";
				el.style.opacity = 0;
				done();
			}, 0);
		},
		afterLeave(el) {
			console.log("After Leave");
		},
		leaveCancelled(el) {
			console.log("Leave Cancelled");
		},
	},
};
</script>

<template>
	<div>
		<button @click="toggleModal">Open Modal</button>
		<transition
			@before-enter="beforeEnter"
			@enter="enter"
			@after-enter="afterEnter"
			@enter-cancelled="enterCancelled"
			@before-leave="beforeLeave"
			@leave="leave"
			@after-leave="afterLeave"
			@leave-cancelled="leaveCancelled"
		>
			<div
				v-if="showModal"
				class="modal-overlay"
			>
				<div class="modal-content">
					<h2>Modal Title</h2>
					<p>This is a modal dialog.</p>
					<button @click="toggleModal">Close</button>
				</div>
			</div>
		</transition>
	</div>
</template>

<style>
.modal-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.5);
	display: flex;
	justify-content: center;
	align-items: center;
}

.modal-content {
	background-color: white;
	padding: 20px;
	border-radius: 5px;
	text-align: center;
}
</style>
