# Angular Firebase Analytics Integration for NG-LOG

[![GitHub Actions Status](https://github.com/DagonMetric/ng-log-firebase-analytics/workflows/Main%20Workflow/badge.svg)](https://github.com/DagonMetric/ng-log-firebase-analytics/actions)
[![npm version](https://badge.fury.io/js/%40dagonmetric%2Fng-log-firebase-analytics.svg)](https://www.npmjs.com/package/@dagonmetric/ng-log-firebase-analytics)
[![Gitter](https://badges.gitter.im/DagonMetric/general.svg)](https://gitter.im/DagonMetric/general?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Firebase Analytics implementation for [DagonMetric/ng-log](https://github.com/DagonMetric/ng-log).

## Getting Started

### Installation

npm

```bash
npm install @dagonmetric/ng-log @dagonmetric/ng-log-firebase-analytics
```

or yarn

```bash
yarn add @dagonmetric/ng-log @dagonmetric/ng-log-firebase-analytics
```

### Module Setup (app.module.ts)

```typescript
import { LogModule } from '@dagonmetric/ng-log';
import { FirebaseAnalyticsLoggerModule } from '@dagonmetric/ng-log-firebase-analytics';

@NgModule({
  imports: [
    // Other module imports

    // ng-log modules
    LogModule,
    FirebaseAnalyticsLoggerModule.configure({
      firebaseConfig : {
          apiKey: '<your_firebase_app_api_key>',
          projectId: '<your_firebase_project_id>',
          appId: '<your_firebase_app_id>',
          // Replace 'G-1111111111' with your measurementId
          measurementId: 'G-1111111111',
          // ...
      }
    })
  ]
})
export class AppModule { }
```

Live edit [app.module.ts in stackblitz](https://stackblitz.com/github/dagonmetric/ng-log-firebase-analytics/tree/master/samples/demo-app?file=src%2Fapp%2Fapp.module.ts)

### Usage (app.component.ts)

```typescript
import { Component, OnInit } from '@angular/core';

import { LogService } from '@dagonmetric/ng-log';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  constructor(private readonly logService: LogService) { }

  ngOnInit(): void {
    // Track traces
    this.logService.trace('Testing trace');
    this.logService.debug('Testing debug');
    this.logService.info('Testing info');
    this.logService.warn('Testing warn');

    // Track exceptions
    this.logService.error(new Error('Testing error'));
    this.logService.fatal(new Error('Testing critical'));

    // Track page view
    this.logService.trackPageView({
      name: 'My Angular App',
      uri: '/home'
    });

    // Track page view with timing
    this.logService.startTrackPage('about');
    this.logService.stopTrackPage('about', { uri: '/about' });

    // Track custom event
    this.logService.trackEvent({
      name: 'video_auto_play_start',
      properties: {
        non_interaction: true
      }
    });

    // Track custom event with metrics
    this.logService.trackEvent({
      name: 'foo',
      custom_map: {
        dimension2: 'age',
        metric5: 'avg_page_load_time'
      },
      measurements: {
        avg_page_load_time: 1
      },
      properties: {
        age: 12
      }
    });

    // Track custom event with timing
    this.logService.startTrackEvent('video_auto_play');
    this.logService.stopTrackEvent('video_auto_play', {
      properties: {
        non_interaction: true
      }
    });

    // Set user properties
    this.logService.setUserProperties('<Authenticated User Id>', '<Account Id>');

    // Clear user properties
    this.logService.clearUserProperties();
  }
}
```

Live edit [app.component.ts in stackblitz](https://stackblitz.com/github/dagonmetric/ng-log-firebase-analytics/tree/master/samples/demo-app?file=src%2Fapp%2Fapp.component.ts)

## Samples

* Demo app [view source](https://github.com/DagonMetric/ng-log-firebase-analytics/tree/master/samples/demo-app) / [live edit in stackblitz](https://stackblitz.com/github/dagonmetric/ng-log-firebase-analytics/tree/master/samples/demo-app)

## Related Projects

* [ng-log](https://github.com/DagonMetric/ng-log) - Angular logging and telemetry service abstractions and some implementations
* [ng-log-applicationinsights](https://github.com/DagonMetric/ng-log-applicationinsights) - Microsoft Azure Application Insights implementation for `ng-log`
* [ng-log-gtag](https://github.com/DagonMetric/ng-log-gtag) - Angular Google Analytics (gtag.js) logger implementation for `ng-log`
* [ng-log-facebook-analytics](https://github.com/DagonMetric/ng-log-facebook-analytics) - Facebook Pixel Analytics implementation for `ng-log`

## Feedback and Contributing

Check out the [Contributing](https://github.com/DagonMetric/ng-log-firebase-analytics/blob/master/CONTRIBUTING.md) page.

## License

This repository is licensed with the [MIT](https://github.com/DagonMetric/ng-log-firebase-analytics/blob/master/LICENSE) license.
