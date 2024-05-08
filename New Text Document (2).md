## Complete New Discord Quest (Genshin Impact Badge)
> [!NOTE]
> برای انجام این کار شما نیاز به نصب برنامه vencord.exe و فعال کردن enable developer react در تنظیمات vencord نیاز هست



1. اول از همه در قسمت Gift inventory میشن رو اکسپت کنید
2. وارد یک ویس شوید
3. با یک یوز دیگر وارد همون ویس بشید
4. یک صفحه دلخواه رو استریم کنید
5. <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>I</kbd> را فشار دهید
6. وارد کنسول بشد
7. /allow pasting را وارد کنید
8. سپس این کد را در آن پیست کنید

```js
let wpRequire;
window.webpackChunkdiscord_app.push([[ Math.random() ], {}, (req) => { wpRequire = req; }]);

let ApplicationStreamingStore = Object.values(wpRequire.c).find(x => x?.exports?.default?.getStreamerActiveStreamMetadata).exports.default;
let QuestsStore = Object.values(wpRequire.c).find(x => x?.exports?.default?.getQuest).exports.default;
let FluxDispatcher = Object.values(wpRequire.c).find(x => x?.exports?.default?.flushWaitQueue).exports.default;

let quest = [...QuestsStore.quests.values()].find(x => x.userStatus?.enrolledAt && !x.userStatus?.completedAt && new Date(x.config.expiresAt).getTime() > Date.now())
let isApp = navigator.userAgent.includes("Electron/")
if(!isApp) {
	console.log("This no longer works in browser. Use the desktop app!")
} else if(!quest) {
	console.log("You don't have any uncompleted quests!")
} else {
	let pid = Math.floor(Math.random() * 30000) + 1000
	ApplicationStreamingStore.getStreamerActiveStreamMetadata = () => ({
		id: quest.config.applicationId,
		pid,
		sourceName: null
	})
	
	let secondsNeeded = quest.config.streamDurationRequirementMinutes * 60
	let fn = data => {
		let progress = data.userStatus.streamProgressSeconds
		console.log(`Quest progress: ${progress}/${secondsNeeded}`)
		
		if(progress >= secondsNeeded) {
			console.log("Quest completed!")
			FluxDispatcher.unsubscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
		}
	}
	FluxDispatcher.subscribe("QUESTS_SEND_HEARTBEAT_SUCCESS", fn)
	
	console.log(`Spoofed your stream to ${quest.config.applicationName}. Stay in vc for ${Math.ceil(quest.config.streamDurationRequirementMinutes - (quest.userStatus?.streamProgressSeconds ?? 0) / 60)} more minutes.`)
	console.log("Remember that you need at least 1 other person to be in the vc!")
}
```

9. به مدت 15 دقیقه این کار رو انجام بدید

## Links

در صورت داشتن مشکل در دیسکورد زیر جوین بشید:
(https://discord.com/invite/EZGmusVR7W)

