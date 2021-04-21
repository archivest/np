<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Login</h2>

          <Notification :message="error" v-if="error" />

          <form class="loginform" method="post" @submit.prevent="login">
            <div class="field">
              <div class="control">
                <input
                  type="email"
                  class="input"
                  name="email"
                  placeholder="Email"
                  v-model="email"
                />
              </div>
            </div>

            <div class="field">
              <div class="control">
                <input
                  type="password"
                  class="input"
                  name="password"
                  placeholder="Password"
                  v-model="password"
                />
              </div>
            </div>

            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">
                Log In
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from "~/components/Notification";
export default {
  middleware: "guest",
  components: {
    Notification,
  },
  data() {
    return {
      email: "",
      password: "",
      error: null,
    };
  },
  methods: {
    async login() {
      try {
        await this.$auth.loginWith("local", {
          data: {
            email: this.email,
            password: this.password,
          },
        });
        this.$router.push("/");
      } catch (e) {
        this.error = e.response.data.message;
      }
    },
  },
};
</script>

<style scoped>
.has-text-centered {
  margin-top: 20px;
}

.loginform {
  margin-top: 20px;
  background: var(--text-input-background-color);
  color: #403868;
  font-weight: 600;
}

.control {
  margin-top: 10px;
}
</style>