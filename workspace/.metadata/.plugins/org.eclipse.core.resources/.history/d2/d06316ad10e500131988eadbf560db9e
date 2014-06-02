package com.dhliwayok.hopeworldwide;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.util.ArrayList;

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.NameValuePair;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.HttpClient;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.DefaultHttpClient;
import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import com.dhliwayok.hopeworldwide.HopeDbAdapter.HopeHelper;
import com.dhliwayok.hopeworldwide.HopeDbAdapter;
import com.dhliwayok.hopeworldwide.LoginActivity;
import com.dhliwayok.hopeworldwide.MainActivity;
import com.dhliwayok.hopeworldwide.Message;
import com.dhliwayok.hopeworldwide.R;
import com.dhliwayok.hopeworldwide.MainActivity.ActivitiesBroadcastReceiver;

import android.support.v7.app.ActionBar;
import android.support.v7.app.ActionBarActivity;
import android.support.v4.app.Fragment;
import android.app.Activity;
import android.app.AlertDialog;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.DialogInterface;
import android.content.Intent;
import android.content.IntentFilter;
import android.database.Cursor;
import android.net.ConnectivityManager;
import android.net.NetworkInfo;
import android.os.Bundle;
import android.os.Handler;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.Menu;
import android.view.MenuItem;
import android.view.View;
import android.view.ViewGroup;
import android.os.Build;

public class MainActivity extends Activity {

	private HopeDbAdapter mydb;  
	private MyConnect connect;
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		
		
		IntentFilter intentFilter = new IntentFilter();
		intentFilter.addAction("CLEAR_STACK");
		BroadcastReceiver r;
		r = new ActivitiesBroadcastReceiver();
		registerReceiver(r, intentFilter);
		
		 mydb= new HopeDbAdapter(this);
		 connect = new MyConnect(mydb);
		 //if(isOnline())
			 connect.execute();
		 //mydb.close();
		 
		// Message.message(this, mydb.displayChildDetails("Kalamba Timba"));
		 
		
		 
		
try {
	new Handler().postDelayed(new Runnable() {
	            @Override
	            public void run() {
	            	if(isOnline()){
	                final Intent mainIntent = new Intent(MainActivity.this, LoginActivity.class);
	                MainActivity.this.startActivity(mainIntent);
	                MainActivity.this.finish();
	            	}else{
	            		AlertDialog.Builder builder1 = new AlertDialog.Builder(MainActivity.this);
	    				builder1.setTitle("Message");
	    				builder1.setMessage("No Internet Connection \nApplication will exit...");
	    				builder1.setCancelable(true);
	    				builder1.setNeutralButton(android.R.string.ok,
	    				        new DialogInterface.OnClickListener() {
	    				    public void onClick(DialogInterface dialog, int id) {
	    				    	Intent broadcastIntent = new Intent();
	    						broadcastIntent.setAction("CLEAR_STACK");
	    						sendBroadcast(broadcastIntent);
	    				    }
	    				});

	    				AlertDialog alert11 = builder1.create();
	    				alert11.show();
	            		
	            	}
	            }
	        }, 7000);//langing page with picture runs for 7seconds
} catch (Exception e) {
	// TODO Auto-generated catch block
	e.printStackTrace();
}

		 
	
	}
	
		

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {

		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.main, menu);
		return true;
	}

	@Override
	public boolean onOptionsItemSelected(MenuItem item) {
		// Handle action bar item clicks here. The action bar will
		// automatically handle clicks on the Home/Up button, so long
		// as you specify a parent activity in AndroidManifest.xml.
		int id = item.getItemId();
		if (id == R.id.action_settings) {
			return true;
		}
		return super.onOptionsItemSelected(item);
	}

	
	class ActivitiesBroadcastReceiver extends BroadcastReceiver {
		
		@Override
		public void onReceive(Context context, Intent intent) {
			// TODO Auto-generated method stub
			finish();
		}
	}
	
	public boolean isOnline() {
	    ConnectivityManager cm =
	        (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE);
	    NetworkInfo netInfo = cm.getActiveNetworkInfo();
	    if (netInfo != null && netInfo.isConnected()) {
	        return true;
	    }
	    return false;
	}


}


