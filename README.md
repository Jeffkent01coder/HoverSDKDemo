## HoverSDKDemo
Hover SDK is an Android SDK that lets mobile developers to add money features to the applications. This SDK does not require an internet connection, it automates USSD sessions under the hood of an android application.

## What is an Action
An Action depicts a path that one follows while using USSD codes. When you create an action, Hover uses it to navigate to the devices USSD menu.

## Init Hover
`Hover.initialize(this)`

## Run the USSD Session
```kotlin
binding.buttonSend.setOnClickListener {
            try {
                val intent = HoverParameters.Builder(this)
                    .request("14c45f2e")  //Action ID
                    .extra("phoneNumber", binding.editTextPhoneNumber.text.toString().trim())
                    .extra("amount", binding.editTextAmount.text.toString().trim())
                    .buildIntent()

                startActivityForResult(intent, 0)
            } catch (e: Exception) {
                Toast.makeText(this@MainActivity, "Hover Error", Toast.LENGTH_SHORT).show()
            }
        }
```

## Listen for USSD Information
```kotlin
override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
        super.onActivityResult(requestCode, resultCode, data)
        try {
            if (requestCode == 0 && resultCode == RESULT_OK) {

                Toast.makeText(
                    this,
                    "You will receive an MPESA Confirmation message shortly",
                    Toast.LENGTH_SHORT
                ).show()

            } else if (requestCode == 0 && resultCode == RESULT_CANCELED) {

                Toast.makeText(this, data?.getStringExtra("error"), Toast.LENGTH_SHORT).show()
                Log.d(TAG, "onActivityResult: ${data?.getStringExtra("error")}")
            }
        } catch (e: Exception) {
            Log.d(TAG, "onActivityResult: ${e.localizedMessage}")
        }
    }
```

## Demo
https://user-images.githubusercontent.com/50293753/131500844-7ad54f1b-60df-4632-bfe6-3ad145a0e632.mp4


