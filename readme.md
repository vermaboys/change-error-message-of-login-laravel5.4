## Change error message of login laravel5.4

You tube==> https://youtu.be/S4BeQVeVXeM

#You can clone this project

run command on terminal "git clone https://github.com/vermaboys/change-error-message-of-login-laravel5.4"

#you can also implement using instructions which is given below

composer create-project laravel/laravel your-project-name

Write sendFailedLoginResponse function in LoginController which is given below

/*
The LoginController uses the AuthenticatesUsers trait which has a method sendFailedLoginResponse which is responsible for the error message redirect upon authentication failure
*/

protected function sendFailedLoginResponse(Request $request)
{

    if ( ! User::where('email', $request->email)->first() ) {
        return redirect()->back()
            ->withInput($request->only($this->username(), 'remember'))
            ->withErrors([
                $this->username() => 'Email address not found',
            ]);
    }

    if ( ! User::where('email', $request->email)->where('password', bcrypt($request->password))->first() ) {
        return redirect()->back()
            ->withInput($request->only($this->username(), 'remember'))
            ->withErrors([
                'password' => 'Incorrect password',
            ]);
    }

}

write code in LoginController which is given below

use Illuminate\Http\Request;

use Auth;

use App\User;