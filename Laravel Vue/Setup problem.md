==hasnat@hasnat-PC:~/Desktop$ laravel new trypos laravel: command not found==

The error:

```
laravel: command not found
```

means that the Laravel installer is not installed or it's not available in your system’s `PATH`.

---

### ✅ To fix this, follow these steps:

#### **Option 1: Install Laravel Installer via Composer (Recommended)**

Run this in your terminal:

```bash
composer global require laravel/installer
```

Then ensure Composer’s global bin directory is in your system `PATH`. Add this to your shell config file (e.g., `.bashrc`, `.zshrc`, or `.bash_profile`):

```bash
export PATH="$HOME/.composer/vendor/bin:$PATH"
# or for newer Composer versions:
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
```

Then reload your terminal or run:

```bash
source ~/.bashrc   # or source ~/.zshrc depending on your shell
```

Now you can try again:

```bash
laravel new trypos
```

---

#### **Option 2: Use Composer Directly (Without Laravel Installer)**

If you don't want to install the Laravel installer, you can create a new project like this:

```bash
composer create-project laravel/laravel trypos
```

This works the same way and is often more version-consistent.

---

Let me know which option you'd prefer, or if you want Laravel installed globally for all future use.

==Option 2 work but 1 not work why ?==

Great question. Here's **why Option 2 worked** and **Option 1 did not**:

---

### ✅ **Why Option 2 Worked**

This command:

```bash
composer create-project laravel/laravel trypos
```

directly downloads Laravel from the Laravel GitHub repository and sets up a full Laravel project. It doesn't depend on the `laravel` command or require any global installer.

So as long as you have **Composer installed**, Option 2 will always work.

---

### ❌ **Why Option 1 Didn't Work**

When you tried:

```bash
laravel new trypos
```

That requires the **Laravel installer** (`laravel`) to be available globally.

If it didn’t work, here are the likely reasons:

1. **You didn’t install it:**
    
    You didn’t run:
    
    ```bash
    composer global require laravel/installer
    ```
    
2. **Installed, but not in PATH:**
    
    Composer may have installed it globally, but your shell can't find it because its location (`~/.composer/vendor/bin` or `~/.config/composer/vendor/bin`) is not in your `PATH`.
    
    You can check if it's installed by running:
    
    ```bash
    ~/.composer/vendor/bin/laravel --version
    # or
    ~/.config/composer/vendor/bin/laravel --version
    ```
    
3. **Composer global bin path varies by system:**
    
    - Older systems: `~/.composer/vendor/bin`
        
    - Newer systems: `~/.config/composer/vendor/bin`
        
    
    So, you must add the correct one to your `PATH` like this:
    
    ```bash
    export PATH="$HOME/.config/composer/vendor/bin:$PATH"
    ```
    
    And then reload your terminal:
    
    ```bash
    source ~/.bashrc
    ```
    

---

### 🧪 Want to test if it’s installed?

Run:

```bash
which laravel
```

If it returns nothing, it's not in your `PATH`.

---

Would you like help configuring Option 1 properly, or are you happy continuing with Option 2?

==hasnat@hasnat-PC:~$ composer global require laravel/installer==
==Changed current directory to /home/hasnat/.config/composer==
==./composer.json has been updated==
==Running composer update laravel/installer==
==Loading composer repositories with package information==
==Updating dependencies==
==Nothing to modify in lock file==
==Writing lock file==
==Installing dependencies from lock file (including require-dev)==
==Nothing to install, update or remove==
==Generating autoload files==
==18 packages you are using are looking for funding.==
==Use the `composer fund` command to find out more!==
==No security vulnerability advisories found.==
==Using version ^5.15 for laravel/installer==

Thanks for sharing that! This shows that the Laravel installer **was installed correctly**, but the issue is still likely with your **`PATH` environment variable**.

---

### ✅ Step-by-Step Fix:

Now that the Laravel installer is installed at:

```
/home/hasnat/.config/composer/vendor/bin/laravel
```

You need to **add that directory to your system `PATH`**.

---

### ✅ 1. Add Laravel to PATH

Open your shell config file (`.bashrc`, `.zshrc`, etc.) in your home directory. For example, if you're using Bash:

```bash
nano ~/.bashrc
```

==Add this line **at the end** of the file:==

```bash
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
```

Then save and exit (`Ctrl + O`, `Enter`, then `Ctrl + X`).

---

### ✅ 2. Reload Your Terminal

Apply the change immediately:

```bash
source ~/.bashrc
```

---

### ✅ 3. Verify Installation

Now check:

```bash
which laravel
```

You should see something like:

```
/home/hasnat/.config/composer/vendor/bin/laravel
```

Then run:

```bash
laravel --version
```

And finally:

```bash
laravel new projectname
```

---

Let me know if it still doesn’t work — we can debug further.![[Screenshot from 2025-06-03 13-52-26.png]]


অবশ্যই! নিচে ব্যাখ্যাটি বাংলায় দেওয়া হলো:

---

তুমি যখন নিচের কমান্ডটি চালাও:

```bash
laravel new projectname
```

তখন Laravel Installer তোমাকে জিজ্ঞাসা করে:

```
Which authentication provider do you prefer?
› ● Laravel's built-in authentication
  ○ WorkOS (Requires WorkOS account)
```

---

### 🔍 এর মানে কী?

Laravel জানতে চায় তুমি তোমার প্রজেক্টে কোন ধরনের **Authentication (লগইন সিস্টেম)** ব্যবহার করতে চাও।

#### ✅ **Laravel's built-in authentication**

- Laravel নিজেই একটি বিল্ট-ইন Authentication সিস্টেম দেয়।
    
- এতে থাকে:
    
    - ইউজার রেজিস্ট্রেশন
        
    - লগইন/লগআউট
        
    - পাসওয়ার্ড রিসেট
        
- এটি **ফ্রি** এবং **সবচেয়ে বেশি ব্যবহৃত**।
    
- এটি `Laravel Breeze`, `Jetstream`, অথবা `Fortify` এর মতো প্যাকেজ ব্যবহার করে।
    

👉 **তুমি যদি সাধারণ ওয়েব অ্যাপ বানাচ্ছো — এই অপশনটাই নাও।**

---

#### 🏢 **WorkOS**

- এটি একটি থার্ড-পার্টি সার্ভিস ([https://workos.com)।](https://workos.xn--com\)-jkj/)
    
- এটি **Enterprise-level SSO (Single Sign-On)** সিস্টেম দেয়:
    
    - Google Workspace, Azure AD, Okta ইত্যাদির মাধ্যমে লগইন।
        
- এটি ব্যবহার করতে হলে তোমার **WorkOS অ্যাকাউন্ট** লাগবে।
    
- সাধারণ প্রজেক্টের জন্য এটি দরকার নেই।
    

👉 এটি শুধুমাত্র ব্যবহার করো যদি তুমি **বড় কোম্পানির SaaS অ্যাপ বানাচ্ছো** এবং তাদের Enterprise Login দরকার হয়।

---

### ✅ তাহলে তুমি কী বেছে নেবে?

**Laravel's built-in authentication** — এটা সবার জন্য যথেষ্ট, সহজ এবং ব্যবহার উপযোগী।

---

চাও কি আমি তোমাকে Laravel Breeze বা Jetstream দিয়ে Authentication সেটআপ করতে শেখাই?


তুমি Laravel Installer ব্যবহার করে `doctorReceft` নামের একটি নতুন Laravel প্রজেক্ট তৈরি করছো এবং এতে Vue.js ও বিল্ট-ইন authentication সিস্টেম যুক্ত করছো। চমৎকার!

এখানে প্রতিটি ধাপের বিস্তারিত **বাংলা ব্যাখ্যা** দেওয়া হলো — যেনো তুমি বুঝতে পারো প্রতিটি অপশন আসলে কী করে:

---

## 🛠️ ১. প্রজেক্ট তৈরি করেছো

```bash
laravel new doctorReceft
```

➡️ এটি একটি নতুন Laravel প্রজেক্ট তৈরি করবে `doctorReceft` নামে।

---

## 🧱 ২. Starter Kit নির্বাচন

```
Which starter kit would you like to install?
› ● None
  ○ React
  ○ Vue
  ○ Livewire
```

➡️ এখানে Laravel জানতে চায় তুমি কোন UI (ইউজার ইন্টারফেস) ফ্রেমওয়ার্ক ব্যবহার করতে চাও:

- **None**: কোন UI Framework লাগবে না।
    
- **React**: React.js দিয়ে UI তৈরি হবে।
    
- **Vue**: Vue.js ব্যবহার করে UI বানানো হবে। ✅ **তুমি এটা বেছে নিয়েছো।**
    
- **Livewire**: Blade টেমপ্লেট + AJAX দিয়ে কাজ করা যায়।
    

✅ তুমি **Vue** বেছে নিয়েছো, মানে Laravel প্রজেক্টে Vue.js যুক্ত হবে এবং JavaScript SPA (Single Page Application)-এর মতো কাজ করবে।

---

## 🔐 ৩. Authentication Provider নির্বাচন

```
Which authentication provider do you prefer?
› ● Laravel's built-in authentication
  ○ WorkOS
```

➡️ এখানে Laravel জানতে চায় লগইন/রেজিস্ট্রেশনের জন্য কোন Authentication সিস্টেম ব্যবহার করতে চাও:

- **Laravel's built-in authentication**: Laravel নিজেই লগইন/সাইনআপ সিস্টেম দিয়ে দিবে (Breeze/Jetstream ব্যবহার করে) ✅ **তুমি এটা নিয়েছো।**
    
- **WorkOS**: Enterprise-level (SSO) লগইনের জন্য, যেমন Google Workspace, Azure AD ইত্যাদি (তোমার দরকার নেই যদি না বড় কোম্পানির সিস্টেম বানাও)।
    

✅ তুমি Laravel's built-in authentication নিয়েছো — এটা সবার জন্য যথেষ্ট।

---

## 🧪 ৪. Testing Framework নির্বাচন

```
Which testing framework do you prefer?
› ● Pest
  ○ PHPUnit
```

➡️ Laravel জানতে চায় তুমি কোন Testing Framework ব্যবহার করতে চাও:

- **Pest**: সুন্দর, নতুন ধরনের টেস্টিং টুল — সহজে লেখা যায়, readable।
    
- **PHPUnit**: Laravel-এর পুরানো ও শক্তিশালী টেস্টিং টুল।
    

✅ তুমি **Pest** বেছে নিয়েছো — এটি আধুনিক ও সহজ টেস্টিং সিস্টেম।

---

## 📦 ৫. JavaScript Dependency Install ও Build

```
Would you like to run npm install and npm run build?
› ● Yes
  ○ No
```

➡️ Laravel জিজ্ঞেস করে, তুমি কি `npm install` ও `npm run build` এখনই চালাতে চাও?

- `npm install`: Vue.js সহ সব JavaScript dependency ইনস্টল করবে।
    
- `npm run build`: Vue ফাইলগুলোকে কম্পাইল করে usable JS বানাবে।
    

✅ তুমি **Yes** বলেছো — মানে Laravel এখনই Vue সেটআপ করে দিবে।

---

## ✅ এখন তুমি যা পেয়েছো:

তোমার `doctorReceft` প্রজেক্টে থাকবে:

- ✅ Laravel 11
    
- ✅ Vue.js ইনস্টল ও কনফিগার করা
    
- ✅ Laravel's built-in authentication (login, register page)
    
- ✅ Pest টেস্টিং ফ্রেমওয়ার্ক
    
- ✅ NPM দিয়ে ফ্রন্টএন্ড build করা
    

---

## 🔄 পরবর্তী পদক্ষেপ

প্রজেক্ট ফোল্ডারে যাও:

```bash
cd doctorReceft
```

সার্ভার চালাও:

```bash
php artisan serve
```

এবং ব্রাউজারে খোলো:  
👉 [http://localhost:8000](http://localhost:8000/)

---

## ✨ Bonus: Vue Component কোথায়?

Vue ফাইলগুলো এখানে থাকবে:

```
resources/js/
```

- `App.vue`: মূল Vue কম্পোনেন্ট
    
- `components/`: এখানে তোমার নিজের কম্পোনেন্ট বানাতে পারো
    

---

## যদি npm না থাকে:

ইনস্টল করতে পারো:

```bash
sudo apt install nodejs npm
```

---

চাও কি আমি Vue Component এর example বা Authentication Page customize করার উপায় দেখাই?