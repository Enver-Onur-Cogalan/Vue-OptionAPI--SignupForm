<template>
  <div class="signup-container">
    <div class="signup-card">
      <div class="card-header">
        <div class="logo-area">
          <div class="logo-circle">
            <svg viewBox="0 0 24 24" fill="currentColor" class="logo-icon">
              <path
                d="M12 2C13.1 2 14 2.9 14 4C14 5.1 13.1 6 12 6C10.9 6 10 5.1 10 4C10 2.9 10.9 2 12 2ZM21 9V7L15 1H5C3.9 1 3 1.9 3 3V17C3 18.1 3.9 19 5 19H11V21C11 21.6 11.4 22 12 22S13 21.6 13 21V19H19C20.1 19 21 18.1 21 17V9Z"
              />
            </svg>
          </div>
        </div>
        <h2 class="title">Hesap Oluştur</h2>
        <p class="subtitle">Hemen başlamak için bilgilerinizi girin</p>
      </div>

      <form @submit.prevent="handleSubmit" class="signup-form">
        <div class="form-group">
          <label for="email" :class="{ active: email || emailFocused }"
            >Email Adresiniz</label
          >
          <div
            class="input-wrapper"
            :class="{ focused: emailFocused, error: emailError }"
          >
            <input
              id="email"
              v-model="email"
              @focus="emailFocused = true"
              @blur="
                emailFocused = false;
                validateEmail();
              "
              type="email"
              :class="{ error: emailError }"
            />
            <div class="input-icon">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M20,8L12,13L4,8V6L12,11L20,6M20,4H4C2.89,4 2,4.89 2,6V18A2,2 0 0,0 4,20H20A2,2 0 0,0 22,18V6C22,4.89 21.1,4 20,4Z"
                />
              </svg>
            </div>
          </div>
          <transition name="error">
            <span v-if="emailError" class="error-message">{{
              emailError
            }}</span>
          </transition>
        </div>

        <div class="form-group">
          <label for="password" :class="{ active: password || passwordFocused }"
            >Şifreniz</label
          >
          <div
            class="input-wrapper"
            :class="{ focused: passwordFocused, error: passwordError }"
          >
            <input
              id="password"
              v-model="password"
              @focus="passwordFocused = true"
              @blur="
                passwordFocused = false;
                validatePassword();
              "
              :type="showPassword ? 'text' : 'password'"
              :class="{ error: passwordError }"
            />
            <button
              type="button"
              @click="showPassword = !showPassword"
              class="password-toggle"
            >
              <svg v-if="showPassword" viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M11.83,9L15,12.16C15,12.11 15,12.05 15,12A3,3 0 0,0 12,9C11.94,9 11.89,9 11.83,9M7.53,9.8L9.08,11.35C9.03,11.56 9,11.77 9,12A3,3 0 0,0 12,15C12.22,15 12.44,14.97 12.65,14.92L14.2,16.47C13.53,16.8 12.79,17 12,17A5,5 0 0,1 7,12C7,11.21 7.2,10.47 7.53,9.8M2,4.27L4.28,6.55L4.73,7C3.08,8.3 1.78,10 1,12C2.73,16.39 7,19.5 12,19.5C13.55,19.5 15.03,19.2 16.38,18.66L16.81,19.09L19.73,22L21,20.73L3.27,3M12,7A5,5 0 0,1 17,12C17,12.64 16.87,13.26 16.64,13.82L19.57,16.75C21.07,15.5 22.27,13.86 23,12C21.27,7.61 17,4.5 12,4.5C10.6,4.5 9.26,4.75 8,5.2L10.17,7.35C10.76,7.13 11.37,7 12,7Z"
                />
              </svg>
              <svg v-else viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M12,9A3,3 0 0,0 9,12A3,3 0 0,0 12,15A3,3 0 0,0 15,12A3,3 0 0,0 12,9M12,17A5,5 0 0,1 7,12A5,5 0 0,1 12,7A5,5 0 0,1 17,12A5,5 0 0,1 12,17M12,4.5C7,4.5 2.73,7.61 1,12C2.73,16.39 7,19.5 12,19.5C17,19.5 21.27,16.39 23,12C21.27,7.61 17,4.5 12,4.5Z"
                />
              </svg>
            </button>
          </div>
          <transition name="error">
            <span v-if="passwordError" class="error-message">{{
              passwordError
            }}</span>
          </transition>
          <div class="password-strength">
            <div class="strength-indicator" :class="passwordStrength.class">
              <div
                class="strength-bar"
                :style="{ width: passwordStrength.width }"
              ></div>
            </div>
            <span class="strength-text">{{ passwordStrength.text }}</span>
          </div>
        </div>

        <div class="form-group">
          <label for="gender" :class="{ active: gender || genderFocused }"
            >Cinsiyet</label
          >
          <div
            class="select-wrapper"
            :class="{ focused: genderFocused, error: genderError }"
          >
            <select
              id="gender"
              v-model="gender"
              @focus="genderFocused = true"
              @blur="
                genderFocused = false;
                validateGender();
              "
              :class="{ error: genderError }"
            >
              <option value="">Seçiniz</option>
              <option value="erkek">Erkek</option>
              <option value="kadin">Kadın</option>
              <option value="diger">Diğer</option>
            </select>
            <div class="select-icon">
              <svg viewBox="0 0 24 24" fill="currentColor">
                <path d="M7,10L12,15L17,10H7Z" />
              </svg>
            </div>
          </div>
          <transition name="error">
            <span v-if="genderError" class="error-message">{{
              genderError
            }}</span>
          </transition>
        </div>

        <!-- ÇOK BASİT CHECKBOX -->
        <div style="margin: 30px 0">
          <div style="display: flex; align-items: center; gap: 10px">
            <input
              type="checkbox"
              v-model="acceptTerms"
              style="width: 16px; height: 16px"
            />
            <span style="font-size: 14px; color: #666">
              Kullanım koşullarını kabul ediyorum
            </span>
          </div>
          <div
            v-if="termsError"
            style="color: #e74c3c; font-size: 12px; margin-top: 5px"
          >
            {{ termsError }}
          </div>
        </div>

        <button
          type="submit"
          class="submit-btn"
          :class="{ loading: isLoading, success: isSuccess }"
          :disabled="isLoading"
        >
          <transition name="button-content" mode="out-in">
            <span v-if="isSuccess" key="success" class="btn-content">
              <svg class="btn-icon" viewBox="0 0 24 24" fill="currentColor">
                <path
                  d="M21,7L9,19L3.5,13.5L4.91,12.09L9,16.17L19.59,5.59L21,7Z"
                />
              </svg>
              Başarılı!
            </span>
            <span v-else-if="isLoading" key="loading" class="btn-content">
              <div class="spinner"></div>
              Kaydediliyor...
            </span>
            <span v-else key="default" class="btn-content">
              <svg class="btn-icon" viewBox="0 0 24 24" fill="currentColor">
                <path d="M19,13H13V19H11V13H5V11H11V5H13V11H19V13Z" />
              </svg>
              Hesap Oluştur
            </span>
          </transition>
        </button>

        <div class="form-footer">
          <p>
            Zaten hesabınız var mı?
            <a href="#" class="login-link">Giriş Yapın</a>
          </p>
        </div>
      </form>
    </div>

    <!-- Background Animation -->
    <div class="bg-animation">
      <div
        class="bg-circle"
        v-for="i in 6"
        :key="i"
        :style="{ animationDelay: i * 2 + 's' }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SignUpForm",
  data() {
    return {
      email: "",
      password: "",
      gender: "",
      acceptTerms: false,
      emailFocused: false,
      passwordFocused: false,
      genderFocused: false,
      showPassword: false,
      emailError: "",
      passwordError: "",
      genderError: "",
      termsError: "",
      isLoading: false,
      isSuccess: false,
    };
  },
  computed: {
    passwordStrength() {
      if (!this.password) return { width: "0%", text: "", class: "" };

      let score = 0;
      if (this.password.length >= 8) score++;
      if (/[a-z]/.test(this.password)) score++;
      if (/[A-Z]/.test(this.password)) score++;
      if (/[0-9]/.test(this.password)) score++;
      if (/[^A-Za-z0-9]/.test(this.password)) score++;

      const levels = [
        { width: "20%", text: "Çok Zayıf", class: "very-weak" },
        { width: "40%", text: "Zayıf", class: "weak" },
        { width: "60%", text: "Orta", class: "medium" },
        { width: "80%", text: "Güçlü", class: "strong" },
        { width: "100%", text: "Çok Güçlü", class: "very-strong" },
      ];

      return levels[Math.max(0, score - 1)] || levels[0];
    },
  },
  methods: {
    validateEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!this.email) {
        this.emailError = "Email adresi gerekli";
      } else if (!emailRegex.test(this.email)) {
        this.emailError = "Geçerli bir email adresi girin";
      } else {
        this.emailError = "";
      }
    },

    validatePassword() {
      if (!this.password) {
        this.passwordError = "Şifre gerekli";
      } else if (this.password.length < 6) {
        this.passwordError = "Şifre en az 6 karakter olmalı";
      } else {
        this.passwordError = "";
      }
    },

    validateGender() {
      if (!this.gender) {
        this.genderError = "Cinsiyet seçimi gerekli";
      } else {
        this.genderError = "";
      }
    },

    validateTerms() {
      if (!this.acceptTerms) {
        this.termsError = "Kullanım koşullarını kabul etmelisiniz";
      } else {
        this.termsError = "";
      }
    },

    async handleSubmit() {
      // Tüm alanları doğrula
      this.validateEmail();
      this.validatePassword();
      this.validateGender();
      this.validateTerms();

      // Hata varsa submit etme
      if (
        this.emailError ||
        this.passwordError ||
        this.genderError ||
        this.termsError
      ) {
        return;
      }

      this.isLoading = true;

      try {
        // API çağrısı simülasyonu
        await new Promise((resolve) => setTimeout(resolve, 2000));

        this.isLoading = false;
        this.isSuccess = true;

        console.log("Form Submitted:", {
          email: this.email,
          password: this.password,
          gender: this.gender,
          acceptTerms: this.acceptTerms,
        });

        // Başarı durumunu 3 saniye sonra sıfırla
        setTimeout(() => {
          this.isSuccess = false;
          this.resetForm();
        }, 3000);
      } catch (error) {
        this.isLoading = false;
        console.error("Kayıt hatası:", error);
      }
    },

    resetForm() {
      this.email = "";
      this.password = "";
      this.gender = "";
      this.acceptTerms = false;
      this.emailError = "";
      this.passwordError = "";
      this.genderError = "";
      this.termsError = "";
    },
  },
};
</script>

<style scoped>
/* Global reset */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}

.signup-container {
  min-height: 100vh;
  width: 100vw;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  position: fixed;
  top: 0;
  left: 0;
  overflow: auto;
}

.bg-animation {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.bg-circle {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 8s infinite linear;
}

.bg-circle:nth-child(1) {
  width: 80px;
  height: 80px;
  top: 20%;
  left: 10%;
}
.bg-circle:nth-child(2) {
  width: 60px;
  height: 60px;
  top: 60%;
  left: 80%;
}
.bg-circle:nth-child(3) {
  width: 100px;
  height: 100px;
  top: 80%;
  left: 20%;
}
.bg-circle:nth-child(4) {
  width: 40px;
  height: 40px;
  top: 10%;
  left: 70%;
}
.bg-circle:nth-child(5) {
  width: 70px;
  height: 70px;
  top: 40%;
  left: 90%;
}
.bg-circle:nth-child(6) {
  width: 50px;
  height: 50px;
  top: 70%;
  left: 5%;
}

@keyframes float {
  0% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(180deg);
  }
  100% {
    transform: translateY(0px) rotate(360deg);
  }
}

.signup-card {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 480px;
  padding: 0;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.card-header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  text-align: center;
  padding: 40px 30px;
}

.logo-area {
  margin-bottom: 20px;
}

.logo-circle {
  width: 80px;
  height: 80px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  backdrop-filter: blur(10px);
}

.logo-icon {
  width: 40px;
  height: 40px;
}

.title {
  font-size: 32px;
  font-weight: 700;
  margin: 0 0 10px 0;
  letter-spacing: -0.5px;
}

.subtitle {
  font-size: 16px;
  opacity: 0.9;
  margin: 0;
  font-weight: 300;
}

.signup-form {
  padding: 40px 30px 30px;
}

.form-group {
  margin-bottom: 25px;
  position: relative;
}

.form-group label {
  position: absolute;
  left: 16px;
  top: 50%;
  transform: translateY(-50%);
  color: #666;
  font-size: 16px;
  font-weight: 500;
  transition: all 0.3s ease;
  pointer-events: none;
  background: white;
  padding: 0 4px;
  z-index: 1;
}

.form-group label.active {
  top: 0;
  font-size: 14px;
  color: #667eea;
  font-weight: 600;
}

.input-wrapper {
  position: relative;
  transition: all 0.3s ease;
}

.input-wrapper input,
.select-wrapper select {
  width: 100%;
  padding: 16px 50px 16px 16px;
  border: 2px solid #e1e5e9;
  border-radius: 12px;
  font-size: 16px;
  background: white;
  transition: all 0.3s ease;
  outline: none;
}

.input-wrapper.focused input,
.select-wrapper.focused select {
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.input-wrapper.error input,
.select-wrapper.error select {
  border-color: #e74c3c;
  box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.1);
}

.input-icon {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  color: #999;
  pointer-events: none;
}

.password-toggle {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  padding: 0;
  width: 20px;
  height: 20px;
  color: #999;
  cursor: pointer;
  transition: color 0.2s;
}

.password-toggle:hover {
  color: #667eea;
}

.password-strength {
  margin-top: 8px;
  display: flex;
  align-items: center;
  gap: 12px;
}

.strength-indicator {
  flex: 1;
  height: 4px;
  background: #f0f0f0;
  border-radius: 2px;
  overflow: hidden;
}

.strength-bar {
  height: 100%;
  transition: all 0.3s ease;
}

.strength-indicator.very-weak .strength-bar {
  background: #e74c3c;
}
.strength-indicator.weak .strength-bar {
  background: #f39c12;
}
.strength-indicator.medium .strength-bar {
  background: #f1c40f;
}
.strength-indicator.strong .strength-bar {
  background: #27ae60;
}
.strength-indicator.very-strong .strength-bar {
  background: #2ecc71;
}

.strength-text {
  font-size: 12px;
  font-weight: 600;
  min-width: 80px;
}

.select-wrapper {
  position: relative;
}

.select-wrapper select {
  appearance: none;
  cursor: pointer;
}

.select-icon {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  width: 20px;
  height: 20px;
  color: #999;
  pointer-events: none;
}

.error-message {
  color: #e74c3c;
  font-size: 12px;
  margin-top: 6px;
  display: block;
  font-weight: 500;
}

.submit-btn {
  width: 100%;
  padding: 16px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  margin: 30px 0 20px;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
}

.submit-btn:disabled {
  cursor: not-allowed;
  opacity: 0.8;
}

.submit-btn.loading {
  background: #95a5a6;
}

.submit-btn.success {
  background: #27ae60;
}

.btn-content {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.btn-icon {
  width: 18px;
  height: 18px;
}

.spinner {
  width: 16px;
  height: 16px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-top: 2px solid white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.form-footer {
  text-align: center;
  margin-top: 20px;
}

.form-footer p {
  color: #666;
  font-size: 14px;
  margin: 0;
}

.login-link {
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.2s;
}

.login-link:hover {
  color: #764ba2;
  text-decoration: underline;
}

/* Transitions */
.error-enter-active,
.error-leave-active {
  transition: all 0.3s ease;
}

.error-enter-from,
.error-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.button-content-enter-active,
.button-content-leave-active {
  transition: all 0.2s ease;
}

.button-content-enter-from,
.button-content-leave-to {
  opacity: 0;
  transform: scale(0.8);
}

/* Responsive */
@media (max-width: 768px) {
  .signup-container {
    padding: 10px;
  }

  .signup-card {
    border-radius: 16px;
  }

  .card-header {
    padding: 30px 20px;
  }

  .title {
    font-size: 28px;
  }

  .signup-form {
    padding: 30px 20px 20px;
  }

  .form-group {
    margin-bottom: 20px;
  }
}

@media (max-width: 480px) {
  .card-header {
    padding: 25px 15px;
  }

  .title {
    font-size: 24px;
  }

  .signup-form {
    padding: 25px 15px 15px;
  }
}
</style>