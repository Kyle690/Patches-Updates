# useAuthHook 
As both login & register screens utilize the same logic and state, it makes sense to use one hook for both.


## Usage
To manipulate state we make use of the dispatch action, in which we want to pass an object with a type and a payload.

Example - Say we want to update the firstName input

```
	const {dispatch, state:{firstName}}=useAuthHook();
	
	<TextInput
		value={firstName}
		onTextChange={(text=)=>dispatch(type:FIRST_NAME,payload:text)}
	/>
	
	
	
```
	
	

## Functions
 
 * ###**onLogin**
 
 	- Used to log user in from state inputs email & password.
 	- Validation
	 	- loginFormValid - bool (false by default)
	 	- loginFormComplete - bool (false by default) 
 	- When called:
	 	-  Sets loading to true. 
	 	-  Logs user in.
	-  If error occurs: 
		-  Sets loading to false
		-  Sets the error to state error.
 
	**Example** - Login Screen
	
	```
		const useAuthHook from '../hooks/useAuthHook;
		
		const SignInScreen=()=>{
		
			const {state:{loading}, onLogin}=useAuthHook();
		
		
			return (
					<View>
							{/* inputs here*/}
							<Button
								title='Login'
								onPress={onLogin}
								loading={loading}
							/>
					</View>
			)
		}
	```
* ### **onRegister**
	- Used to register a user once they have completed all fields.
	- Validation
		* registrationFormValid - bool (false by default)
		* registrationFormComplete - bool 	(false by default)
	- When called: 
		* sets loading to true. 
		* Registers user.
		*  registration success, the user is then logged in.
	- If an error occurs:
		* sets loading to false and sets the error to state error.
		* If an error occurs with error.code of UsernameExists:
			*  sets loading to false,
			*   error to state.emailError 
			*    duplicateUser to true. 	

	Example
 	
 	```
 	const useAuthHook from '../hooks/useAuthHook;
 	
 	const signUpScreen=()=>{
 		const {state:{loading}, onRegister, registrationFormValid registrationFormComplete }=useAuthHook();
 		
 		return (
 			<View>
 				{/* all inputs here*/}
 				
				<Button
					disabled={registrationFormValid && registrationFormComplete}
					title='Register'
					onPress={onRegister}
					loading={loading}
				/>
 			</View>
 		)
 		
 	}
 ```
 
 ## State - Default
 * firstName : string
 * firstNameInputted : bool
 * firstNameError : null || string
 * lastName : string
 * lastNameInputted : bool
 * lastNameError : null || string
 * email : string
 * emailInputted : bool
 * emailError : null || string
 * duplicateUser : bool
 * password : string
 * passwordInputted : bool 
 * passwordError: null || string
 * confirmPassword : string
 * confirmPasswordInputted : bool
 * confirmPasswordError : null || string
 * activeInput : null || currentInputRef
 * error: null
 * loading: bool
 