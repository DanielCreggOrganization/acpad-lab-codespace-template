# Lab - Week 2 : Introduction to Ionic Angular Apps

---

## **Objectives**

- **Set up** your Ionic Angular development environment.
- **Build** your first Ionic Angular app.
- **Add** new components and modules to an Ionic Angular app.
- **Understand** the structure of an Ionic Angular app.

---

## **Procedure**

### **1. Set Up Your Development Environment**

#### **a. Access Your Codespace**

- Navigate to the **course Moodle page**.
- Locate the **Required Software** section.
- Click on the link to your **Codespace for Labs**.

#### **b. Verify Installed Tools**

Ensure you have the latest versions of the following tools installed:

- **Node.js**
- **npm** (Node Package Manager)
- **TypeScript**
- **Ionic CLI**

Run the following commands in the terminal to check the installed versions:

```bash
node -v
npm -v
tsc -v
ionic -v
```

**Expected Output Example:**

```bash
$ node -v
v16.13.0

$ npm -v
8.1.0

$ tsc -v
Version 4.5.2

$ ionic -v
6.18.1
```

- If any of the tools are missing or outdated, install or update them:
  - **Node.js and npm:** [Download and install from the official website](https://nodejs.org/).
  - **TypeScript:** Install globally using `npm install -g typescript`.
  - **Ionic CLI:** Install globally using `npm install -g @ionic/cli`.

---

### **2. Create a New Ionic Angular App**

**Note:** Do **not** use the graphical App Creation Wizard.

#### **a. Start a New Project**

In the terminal, run:

```bash
ionic start
```

#### **b. Configure Project Settings**

The Ionic CLI will prompt you for the following information:

- **Framework:** Select **Angular**.
- **Project Name:** Enter `lab1-structure`.
- **Starter Template:** Choose **blank**.
- **Component Type:** Select **NgModules**.

This will create a new Ionic Angular app with the specified settings.

#### **c. Navigate to the Project Directory**

Change directory into your new project:

```bash
cd lab1-structure
```

---

### **3. Explore the Project Structure**

Understanding the structure of an Ionic Angular app is crucial.

#### **a. Entry Point: `main.ts`**

- Located at `src/main.ts`.
- Responsible for bootstrapping the Angular module.
- Imports `AppModule` from `app.module.ts`.

**Content of `main.ts`:**

```typescript
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

#### **b. Root Module: `AppModule`**

- Defined in `src/app/app.module.ts`.
- Acts as the root module of the application.
- Imports necessary modules and declares components.

**Content of `app.module.ts`:**

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouteReuseStrategy } from '@angular/router';

import { IonicModule, IonicRouteStrategy } from '@ionic/angular';

import { AppComponent } from './app.component';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  declarations: [AppComponent],
  entryComponents: [],
  imports: [
    BrowserModule,
    IonicModule.forRoot(),
    AppRoutingModule
  ],
  providers: [
    { provide: RouteReuseStrategy, useClass: IonicRouteStrategy }
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

#### **c. Root Component: `AppComponent`**

- Defined in `src/app/app.component.ts`.
- The top-level component displayed when the app launches.
- Contains the main template for page components.

**Content of `app.component.ts`:**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
})
export class AppComponent {}
```

---

### **4. Build and Serve the App**

Run the following command to start the Ionic development server:

```bash
ionic serve
```

- The app should automatically open in your default web browser at `http://localhost:8100`.
- The development server supports **live reloading**, so changes will reflect in real-time.

---

### **5. Modify the Home Page**

#### **a. Rename the Title to "Home"**

Open `src/app/home/home.page.html` and modify the title:

```html
<ion-header>
  <ion-toolbar>
    <ion-title>Home</ion-title>
  </ion-toolbar>
</ion-header>
```

#### **b. Add a Button to Trigger an Alert**

**Import `AlertController`:**

In `src/app/home/home.page.ts`, add the import statement:

```typescript
import { Component } from '@angular/core';
import { AlertController } from '@ionic/angular';
```

**Modify the `HomePage` Class:**

```typescript
export class HomePage {
  constructor(private alertController: AlertController) {}

  async presentAlert() {
    const alert = await this.alertController.create({
      header: 'Alert',
      subHeader: 'Notification',
      message: 'This is an alert message.',
      buttons: ['OK'],
    });

    await alert.present();
  }
}
```

**Update the Template:**

In `home.page.html`, add the button:

```html
<ion-content>
  <ion-button (click)="presentAlert()">Show Alert</ion-button>
</ion-content>
```

- Save the files and observe the changes in your browser.
- Clicking the button should display an alert.

---

### **6. Add a New Page to the App**

#### **a. Generate a New Page Called "About"**

Use the Ionic CLI to create a new page:

```bash
ionic generate page about
```

- This creates a new directory `src/app/about` with the necessary files.

#### **b. Add Content to the About Page**

Open `src/app/about/about.page.html` and add:

```html
<ion-header>
  <ion-toolbar>
    <ion-title>About</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content>
  <p>Welcome to the About Page!</p>
</ion-content>
```

---

### **7. Navigate Between Pages**

#### **a. Import `NavController`**

In `src/app/home/home.page.ts`, import `NavController`:

```typescript
import { NavController } from '@ionic/angular';
```

#### **b. Update the `HomePage` Class**

```typescript
export class HomePage {
  constructor(
    private alertController: AlertController,
    private navCtrl: NavController
  ) {}

  // Existing presentAlert() method...

  goToAbout() {
    this.navCtrl.navigateForward('/about');
  }
}
```

#### **c. Add a Navigation Button**

In `home.page.html`, add:

```html
<ion-content>
  <!-- Existing alert button -->
  <ion-button (click)="presentAlert()">Show Alert</ion-button>

  <!-- New navigation button -->
  <ion-button (click)="goToAbout()">Go to About Page</ion-button>
</ion-content>
```

- Clicking **Go to About Page** should navigate to the About page.

---

### **8. Explore Ionic UI Components**

Visit the [Ionic Framework Components](https://ionicframework.com/docs/components) page.

#### **a. Add a UI Component to the About Page**

For example, add an **Ionic Card**:

```html
<ion-header>
  <ion-toolbar>
    <ion-title>About</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content>
  <ion-card>
    <ion-card-header>
      <ion-card-title>About This App</ion-card-title>
    </ion-card-header>
    <ion-card-content>
      This app is built using Ionic and Angular.
    </ion-card-content>
  </ion-card>
</ion-content>
```

- Experiment with other components like **Buttons**, **Lists**, or **Grids**.

---

### **9. Commit and Sync Your Work**

#### **a. Initialize Git (If Not Already Initialized)**

```bash
git init
```

#### **b. Add Files to Staging**

```bash
git add .
```

#### **c. Commit Your Changes**

```bash
git commit -m "Completed Lab 1: Initial setup and added about page"
```

#### **d. Push to GitHub**

Ensure your local repository is linked to your GitHub repo.

```bash
git remote add origin https://github.com/your-username/lab1-structure.git
git branch -M main
git push -u origin main
```

---

## **Additional Notes**

- **Live Reloading:** The Ionic development server automatically reloads the app when changes are detected.
- **Exploration:** Feel free to explore more components and customize your app.
- **Documentation:** Refer to the [Ionic Documentation](https://ionicframework.com/docs/) for more information.

---

## **Conclusion**

You have successfully:

- Set up your Ionic Angular environment.
- Built and served your first Ionic Angular app.
- Modified the home page and added interactivity.
- Created a new page and navigated between pages.
- Explored Ionic UI components.
- Committed your work to a GitHub repository.

This foundational knowledge prepares you for more advanced Ionic and Angular development in future labs.

---

**End of Lab 1**

---
