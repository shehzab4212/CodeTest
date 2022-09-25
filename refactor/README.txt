This readme file is related to only refactoring code.

# Bad Things In code

"$request->get('user_id')" You are using this in BookingController line no 38 this is not wrong but if you are following the latest version so use 
the code as per latest version so you can easily access the id without get function like this "$request->user_id"

Dont need to get the role ids from env get the role id from user modal using constant and if role id is confidential. I created a model for only constant example
so dont need to get the role id from the env add this env variable in config/app.php with defaut value and then get the role id using config('app.admin_role_id')

__authenticatedUser if you are getting this variable from the request for checking the user type and etc so dont need to do this just get the Auth::user() in the controller fucntion for getting the current
authenticated user

If BookingController routes in authencation middleware so dont need to check user is login or not if BookingController routes is not in the middleware so need to check the user is login or not for validating the user

If we are using the laravel request so we dont need to apply php core functions the request has also except function so we dont need to apply this "array_except($data, ['_token', 'submit'])"
the actual correct code is "$request->except(['_token', 'submit'])"

In Eloqunt Query or Query Builder where function "where('job_id','=',$jobid)" this means where job_id is equal to $jobId but you need to pass this sign in '=' second parameter by default is equal sign so dont need to add this
parameter in query

"Distance::where('job_id',$jobid)->update(array('distance' => $distance, 'time' => $time));" you are using the bulk update for this update you must need to make sure this udate columns must me in fillable and dont create the array like this "array()"
just add this update fields in array brackets like this  
"Distance::where('job_id',$jobid)->update(['distance' => $distance, 'time' => $time]);"

In this code  
"if(isset($data['admincomment']) && !$data['admincomment'])
{
    return "Please, add comment";
}"
you are returning the error message but after this code you are again getting the admin comment and check if admin comment has value so add in a variable otherwise variable is null

"env('CUSTOMER_ROLE_ID')" You are getting CUSTOMER_ROLE_ID from .env directly you need to create a user config file in config folder for this type of data if the data is confidential otherwise
create the roles constant in the user model


"$msg_text = array(
        "en" => 'Tyvärr har ingen tolk accepterat er bokning: (' . $language . ', ' . $job->duration . 'min, ' . $job->due . '). Vänligen pröva boka om tiden.'
    );"
This method is not wrong but this is not good as well you can simply do this for create an array with en value example below

"$msg_text['en'] = 'Tyvärr har ingen tolk accepterat er bokning: (' . $language . ', ' . $job->duration . 'min, ' . $job->due . '). Vänligen pröva boka om tiden.';"

"->where('cancel_at', Null)" This is not wrong but you can use laravel whereNull function for this and if you need to use this query multiple times so create a scope in the model for this

If you have the model of the table so you dont need to use "DB::table('users')" like this in the query just directly user "User::" and append your query in this

I created the s
I checked all the code of BookingController and BookingController

The variable names is in this code is "snake_case" this is not bad but "thisIsDromedaryCamelCase" if you are using this case so its more good this is my suggestion I did not do this in the code but I suggest this.


# Good Things

You are using repository pattern in the controller so its good
You are using the models for the queries its good
You are using the separte function for all the tasks this means you code is good and if you need the same code in the other fucntion so you just need to call the functions its means your code is reuseable
You are using the conditions for validations and saving or updating the data and other tasks.
For short conditions you are using ternary if else so its also good Things
You are using the carbon for time and date conditions and converting the data as well 
Return the data with success and fail messages
Some more good things as well