- cookies
- stored in browser  
vs
- session
- stored in server

steps:
1. create session controller
2. create sessions
	- Using function helper session(<session_name>,<session_value>).
	- Via the $request->session()->put(<session_name>,<session_value>) method of the Request object.
	- Via the Session::put(<session_name>,<session_value>) method of the Session facade.
3. read sessions
	- Using function helper session(<session_name>).
	- Via the $request->session()->get(<session_name>) method of the Request object.
	- Via Session::get(<session_name>) method of Session facade.
4. delete sessions
	- Using the session->forget(<session_name>) helper function.
	- Via the $request->session()->forget(<session_name>) method of the Request object.
	- Via the Session::forget(<session_name>) method of the Session facade.
5. try flash sessions (immediately deleted after accessing once)
	- Using function helper session()->flash(<session_name>,<session_value>)
	- Via the $request->session()->flash(<session_name>,<session_value>) method of Request object
	- Via Session::flash(<session_name>,<session_value>) method of Session facade