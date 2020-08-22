
<?php

namespace App\Http\Middleware;

use Closure;
use Session;
class CustomAuth
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        //echo "hem";
        $path=$request->path();
        if(($path=="login" || $path=="register") && Session::get('user'))
        {
            return redirect('/');
        }
        else if(($path!="login" && !Session::get('user')) &&($path!="register" && !Session::get('user')))
        {
            return redirect('login');
        }
        return $next($request);
    }
}
login.blade.php
@extends('layout')
@section('content')
<div>
<h1>Use Register Page</h1>

<div class="col-sm-6">
<form method="post" action="login">
@csrf
  
  <div class="form-group">
    <label>Gmail</label>
    <input type="text" class="form-control"  placeholder="Enter gmail" name="gmail">
  </div>
  <div class="form-group">
    <label>Password</label>
    <input type="password" class="form-control"  placeholder="Enter password" name="password">
  </div>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
</div>
</div>
@stop
