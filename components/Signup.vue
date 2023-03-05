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
					color="primary"
				>
					<v-toolbar-title
						class="ma-0 pa-0"
						style="font-size:17px;min-width:100%"
					>
						Ya tienes cuenta?
						<a
							class="link"
							@click="$router.push('/login')"
							style="font-weight:bold;color:white"
						>
							Ingresa aquí
						</a>
							</v-toolbar-title>
							<v-spacer></v-spacer>
						</v-toolbar>
					<v-card-text>	
						<v-toolbar-title
							class="ma-0 my-3 pa-0"
							align="center"
							style="min-height:50px;line-height:22px"
						>
							Registro <br>
							<span style="font-size:17px">de usuario nuevo</span>
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
									:rules="rules.name"
									background-color="#202020"
									required
									color="primary"
									name="firstname"
									label="Nombre"
									type="text"
									v-model="firstName"
								>
								</v-text-field>
								<v-text-field
									:rules="rules.name"
									background-color="#202020"
									color="primary"
									name="lastname"
									label="Apellido"
									type="text"
									v-model="lastName"
									>
								</v-text-field>
								<v-text-field
								:rules="rules.emailRules"
								background-color="#202020"                                                
								color="primary"
								name="email"
								label="Correo electrónico"
								type="text"
								v-model="email"
								>
								</v-text-field>
								<v-text-field
									:rules="rules.password"
									background-color="#202020" 
									color="primary"
									id="password"
									name="password"
									label="Contraseña"
									type="password"
									v-model="password"
								>
								</v-text-field>
								<v-text-field
									:rules="rules.contraseñaRepeat"
									background-color="#202020"
									color="primary"
									id="repeatpassword"
									name="repeatpassword"
									label="Repite Contraseña"
									type="password"
									v-model="repeatpassword"
								>
								</v-text-field>
							</v-form>
							<v-card-actions
								class="ma-0 pa-0 justify-center"
								style="width:100%"
							>
									<v-btn 
										height="50px"
										variant="tonal"
										color="primary" 
										@click="loginHandler"
										style="min-width:100%"
									>
										regístrate
									</v-btn>
							</v-card-actions>
						</v-row>
					</v-card-text>
				</v-card>
			</v-col>
		</v-container>
</template>
 
<script>
	export default {
		name: 'Signup',
		data() {
			return {
				firstName: null,
				lastName: null,
				email: null,
				password: null,
				repeatpassword: null,
				rules: {},
			}
    	},
    	methods: {
			signupHandler() {
				this.rules = {
					name: [
						v => !!v || 'Requerido',
					],
					emailRules: [
						v => !!v || 'Requerido',
						v => !v || /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail inválido'
					],
					password: [
						v => !!v || 'Requerido',
						// v => v.length >= 8 || 'Mínimo 8 caracteres',
						// v => v.length <= 16 || 'Máximo 16 caracteres'
					],
					contraseñaRepeat: [
						v => !!v || 'Requerido',
						v => v === this.password || 'Las contraseñas no coinciden'
					],
				}
				this.$nextTick(() => {
					if(this.$refs.signupForm.validate()) {
						this.$axios.post('/auth/registro', {
							name: this.firstName,
							lastname: this.lastName,
							email: this.email,
							password: this.password
						})
						.then((response) => {
							console.log(response);
							//this.$router.push('/login');
						})
						.catch((error) => {
							console.log(error);
						});
					}
				})
			}
 		}
	}	
</script>

<style lang="sass">

</style>