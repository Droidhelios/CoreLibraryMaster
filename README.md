# ModulesAndroid
Modules usage list

#

# CoreLibraryMaster

## Setup


Add this to your project build.gradle
``` gradle
allprojects {
    repositories { 
        maven {
            credentials {
                username 'droidhelios'
                password 'ZGVkDp8VuHwW62frHkRH'
            }
            url 'https://jitpack.io'
        }
    }
}
```
Add this to your module build.gradle

```gradle
   dependencies {
        implementation 'org.bitbucket.droidhelios:corelibrarymaster:2.6'
    }

```
### Usage
Initilise ConfigLibrary before it use
```java 
    ConfigLibrary.newInstance(context, APPLICATION_KEYWORD)
                .setTestVersion("0.1")
                .setBaseUrl("http://dennislab.com/index.php/Android/");
```

Login configuration
```java

     private void initilizeLogin() {
        LoginSdk.newInstance(MainActivity.this, true)
                .setUrlSignup(ConfigLibrary.BASE_URL + "UserModule/signup")// for corporate Login use method .setUrlLoginCorporate("UserModule/loginCorporate")
                .setUrlLogin(ConfigLibrary.BASE_URL + "UserModule/login")
                .setUrlChangePassword(ConfigLibrary.BASE_URL + "UserModule/changePassword")
                .setUrlForgotPassword(ConfigLibrary.BASE_URL + "UserModule/forgotPassword")
                .setUrlValidateForgotPassword(ConfigLibrary.BASE_URL + "UserModule/validateforgotPassword");
        LoginSdk.getInstance().startActivityForResult(MainActivity.this);
    }
        
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == INTENT_LOGIN && resultCode == RESULT_OK) {
            String userId = data.getStringExtra(LoginActivity.DATA_USER_ID);
            String name = data.getStringExtra(LoginActivity.DATA_USER_NAME);
            String email = data.getStringExtra(LoginActivity.DATA_USER_EMAIL);
            String password = data.getStringExtra(LoginActivity.DATA_USER_PASSWORD);
        }
    }
```

Setup Navigation Drawer
```java

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_drawer); // change layout to activity_drawer
        initDrawerUi("Core Library"); 
    }
    private void initDrawerUi(String title) {
        final DrawerLayout drawer = (DrawerLayout) findViewById(R.id.drawer_layout);
        ImageView ivProfile = (ImageView) findViewById(R.id.iv_profile);
        TextView tvName = (TextView) findViewById(R.id.tv_profile_name);
        NavigationView navigationView = (NavigationView) findViewById(R.id.nav_view);
        Toolbar toolbar = (Toolbar) findViewById(com.dennislabs.corelibrary.R.id.toolbar);
        toolbar.setTitle(title);
        setSupportActionBar(toolbar);
        setDrawer(toolbar, drawer, ivProfile, tvName, navigationView, false, new NavigationView.OnNavigationItemSelectedListener() {
            @Override
            public boolean onNavigationItemSelected(@NonNull MenuItem item) {
                //        // Handle navigation view item clicks here.
                int id = item.getItemId();

                if (id == R.id.nav_item_1) {

                } else if (id == R.id.nav_item_2) {

                } else if (id == R.id.nav_item_3) {

                } else if (id == R.id.nav_item_4) {

                }else if (id == R.id.nav_item_5) {
                    addFragment(AppFeedback.newInstance("userId"), "appFeedback");
                } else if (id == R.id.nav_item_6) {
                    addFragment(AppAboutUs.newInstance(MainActivity.this,""), "appAboutUs");
                } else if (id == R.id.nav_item_7) {
                    Sharewere.shareApp(MainActivity.this);
                }

                drawer.closeDrawer(GravityCompat.START);
                return true;
            }
        });
    }

```

