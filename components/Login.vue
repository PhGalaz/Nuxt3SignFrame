<template>
	<v-container
		fluid
		align="center"
		style="height:calc(100vh - 64px)"
	>
		<v-col
			class="v-col-xs-12 v-col-sm-10 v-col-md-8 v-col-lg-5 v-col-xl-4 align-center"
			style="position:relative;top:50%;transform:translateY(-50%);overflow: hidden"
		>
			<v-card
				justify="center"
				class="elevation-12"
			>
				<v-toolbar 
					dense
					color="secondary"
				>
					<v-toolbar-title
						class="ma-0 pa-0"
						style="font-size:17px;min-width:100%;color:white"
					>
						No tienes cuenta? 
						<a
							class="link"
							@click="$router.push('/signup')"
							style="font-weight:bold;color:white"
						>
							Regístrate
						</a>
					</v-toolbar-title>
				</v-toolbar>
				<v-card-text>
					<v-toolbar-title
						class="ma-0 my-3 pa-0"
						align="center"
						style="min-height:50px;line-height:22px"
					>
						Acceso Clientes
					</v-toolbar-title>
					<v-row
						class="ma-0 pa-0"
						justify="center"
					>
						<v-form
							style="width:100%"
							ref="signupForm"
							lazy-validation 
							eager
						>
							<v-text-field
								color="secondary"
								background-color="#202020"
								name="email"
								label="Email"
								type="text"
								v-model="email"
							></v-text-field>
							<v-text-field
								color="secondary"
								background-color="#202020"
								id="password"
								name="password"
								label="Password"
								type="password"
								v-model="password"
							></v-text-field>
						</v-form>
					</v-row>
					<v-card-actions
						class="ma-0 pa-0 justify-center"
						style="width:100%"
					>
						<v-btn 
							height="50px"
							variant="tonal"
							color="secondary" 
							@click="loginHandler"
							style="min-width:100%"
						>
							Login
						</v-btn>
					</v-card-actions>
				</v-card-text>
			</v-card>
		</v-col>
	</v-container>
</template>

<script>
	export default {
		name: 'Login',
		data() {
			return {
					email: 'felipe@galaz.de',
					password: '123456789'
			}
		},
		methods: {

			async loginHandler() {
				const data = { email: this.email, password: this.password }
				console.log(data);
				try{
						const response = await this.$auth.loginWith('local', { data: data })
						// console.log(response)
						this.$auth.$storage.setUniversal('email', response.data.client.email)
						await this.$auth.setUserToken(response.data.token, response.data.refresh_token)
						// console.log(this.$auth.loggedIn)
					} catch(e) {
						console.log(e.message)
				}
			}
		}
	};
</script>
 
<style lang="sass">
	.v-btn__content
		color: white
		font-weight: bold
</style>