<template>
	<span class="seventv-announce-message-container" :class="className">
		<div class="announce-header">
			<div class="announce-icon">
				<TwAnnounce />
			</div>
			<div class="announce-title">
				<template v-if="msgData.sourceData"> {{ msgData.sourceData.displayName }}'s </template>
				Announcement
			</div>
		</div>
		<div class="announce-message">
			<slot />
		</div>
	</span>
</template>

<script setup lang="ts">
import { useChannelContext } from "@/composable/channel/useChannelContext";
import { useChatProperties } from "@/composable/chat/useChatProperties";
import TwAnnounce from "@/assets/svg/twitch/TwAnnounce.vue";

const props = defineProps<{
	msgData: Twitch.AnnouncementMessage;
}>();

const ctx = useChannelContext();
const properties = useChatProperties(ctx);

const className =
	"announcement-line--" +
	(props.msgData.color == "PRIMARY" && properties.primaryColorHex == null
		? "purple"
		: props.msgData.color.toLowerCase());
</script>

<style scoped lang="scss">
.seventv-announce-message-container {
	display: block;
	border-image-slice: 1;
	border-left: 0.8rem solid;
	border-right: 0.8rem solid;
	margin-top: 0.5rem;
	margin-bottom: 0.5rem;
	overflow-wrap: anywhere;
	background-color: hsla(0deg, 0%, 50%, 5%);

	.announce-header {
		background-color: hsla(0deg, 0%, 50%, 15%);
		padding: 0.5rem 0.5rem 0.5rem 1rem;
		display: flex;

		.announce-icon {
			display: inline-flex;
			padding: 0 0.5rem;
		}

		.announce-title {
			font-weight: 600;
		}
	}

	.announce-message {
		padding: 0.5rem 1.2rem;
	}
}

/* stylelint-disable-next-line selector-class-pattern */
.announcement-line--primary {
	border-color: var(--seventv-channel-accent, currentColor);
}
</style>
