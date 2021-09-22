# onesignal-ngx
Angular OneSignal Plugin: Make it easy to integrate OneSignal with your Angular App!

This is a JavaScript module that can be used to easily include [OneSignal](https://onesignal.com/) code in a website or app that uses Angular for its front-end codebase.

OneSignal is the world's leader for Mobile Push Notifications, Web Push, and In-App Messaging. It is trusted by 1,300,000+ businesses to send 5 billion Push Notifications per day.

You can find more information on OneSignal [here](https://onesignal.com/).

## Contents
- [Install](#install)
- [Usage](#usage)
- [API](#onesignal-api)
- [Advanced Usage](#advanced-usage)

---
## Install

### Yarn

```bash
yarn add onesignal-ngx
```

### npm

```bash
npm install --save onesignal-ngx
```

---
## Library setup
```js
import { OneSignalService } from 'onesignal-ngx';
```

Initialize OneSignal with your `appId` via the `options` parameter:

```js
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'angular-example-app';

  constructor(private oneSignal: OneSignalService) {
    this.oneSignal.init({
      appId: "8e7fe838-fbcd-4152-980d-32565a2dcf03",
    });
  }
}
```

The `init` function returns a promise that resolves when OneSignal is loaded.

**Examples**
```js
await this.oneSignal.init({ appId: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' });
// do other stuff
```

```js
this.oneSignal.init({ appId: 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx' }).then(() => {
  // do other stuff
});
```

### Options
You can pass other [options](https://documentation.onesignal.com/docs/web-push-sdk#init) to the `init` function. Use these options to configure personalized prompt options, auto-resubscribe, and more.

**Service Worker Params**
You can customize the location and filenames of service worker assets. You are also able to specify the specific scope that your service worker should control. You can read more [here](https://documentation.onesignal.com/docs/onesignal-service-worker-faq#sdk-parameter-reference-for-service-workers).

In this distribution, you can specify the parameters via the following:
| Field                      | Details                                                                                                                |
|----------------------------|------------------------------------------------------------------------------------------------------------------------|
| `serviceWorkerParam`       | Use to specify the scope, or the path the service worker has control of.  Example:  `{ scope: "/js/push/onesignal/" }` |
| `serviceWorkerPath`        | The path to the service worker file.                                                                                   |
| `serviceWorkerUpdaterPath` | The path to the service worker updater file.                                                                           |

---
## OneSignal API
### Typescript
This package includes Typescript support.

```ts
class OneSignalService {
  init(options: IInitObject): Promise<void>;
  on(event: string, listener: Function): void;
  off(event: string, listener: Function): void;
  once(event: string, listener: Function): void;
  isPushNotificationsEnabled(callback?: Action<boolean>): Promise<boolean>;
  showHttpPrompt(options?: AutoPromptOptions): Promise<void>;
  registerForPushNotifications(options?: RegisterOptions): Promise<void>;
  setDefaultNotificationUrl(url: string): Promise<void>;
  setDefaultTitle(title: string): Promise<void>;
  getTags(callback?: Action<any>): Promise<void>;
  sendTag(key: string, value: any, callback?: Action<Object>): Promise<Object | null>;
  sendTags(tags: TagsObject<any>, callback?: Action<Object>): Promise<Object | null>;
  deleteTag(tag: string): Promise<Array<string>>;
  deleteTags(tags: Array<string>, callback?: Action<Array<string>>): Promise<Array<string>>;
  addListenerForNotificationOpened(callback?: Action<Notification>): Promise<void>;
  setSubscription(newSubscription: boolean): Promise<void>;
  showHttpPermissionRequest(options?: AutoPromptOptions): Promise<any>;
  showNativePrompt(): Promise<void>;
  showSlidedownPrompt(options?: AutoPromptOptions): Promise<void>;
  showCategorySlidedown(options?: AutoPromptOptions): Promise<void>;
  showSmsSlidedown(options?: AutoPromptOptions): Promise<void>;
  showEmailSlidedown(options?: AutoPromptOptions): Promise<void>;
  showSmsAndEmailSlidedown(options?: AutoPromptOptions): Promise<void>;
  getNotificationPermission(onComplete?: Function): Promise<NotificationPermission>;
  getUserId(callback?: Action<string | undefined | null>): Promise<string | undefined | null>;
  getSubscription(callback?: Action<boolean>): Promise<boolean>;
  setEmail(email: string, options?: SetEmailOptions): Promise<string | null>;
  setSMSNumber(smsNumber: string, options?: SetSMSOptions): Promise<string | null>;
  logoutEmail(): Promise<void>;
  logoutSMS(): Promise<void>;
  setExternalUserId(externalUserId: string | undefined | null, authHash?: string): Promise<void>;
  removeExternalUserId(): Promise<void>;
  getExternalUserId(): Promise<string | undefined | null>;
  provideUserConsent(consent: boolean): Promise<void>;
  getEmailId(callback?: Action<string | undefined>): Promise<string | null | undefined>;
  getSMSId(callback?: Action<string | undefined>): Promise<string | null | undefined>;
  sendOutcome(outcomeName: string, outcomeWeight?: number | undefined): Promise<void>;
}
```

### OneSignal API
See the official [OneSignal WebSDK reference](https://documentation.onesignal.com/docs/web-push-sdk) for information on all available SDK functions.

---
## Advanced Usage
### Events and Event Listeners
You can also listen for native OneSignal events like `subscriptionChange`.

**Example**
```js
this.oneSignal.on('subscriptionChange', function(isSubscribed) {
  console.log("The user's subscription state is now:", isSubscribed);
});
```

See the [OneSignal WebSDK Reference](https://documentation.onesignal.com/docs/web-push-sdk) for all available event listeners.

Enjoy!