Conekta Android
===============

Conekta SDK for Android is a simple resource for make calls to conekta.

This is a library project which makes the life much easier by coding less code for you can do requests for the transactions to credit card, bank and oxxo.

Sample app: 

<a href="https://play.google.com/store/apps/details?id=mx.yellowme.sample">
  <img alt="Get it on Google Play"
       src="https://developer.android.com/images/brand/en_generic_rgb_wo_45.png" />
</a>

API LEVEL Up 8

## Setup Project
1. Clone [conekta-android](https://github.com/javikin/conekta-android.git) it. Then, import the project to your workspace.
 
2. Add reference from `conekta-android` project to **your app**.

    ![Screenshot](https://raw.github.com/javikin/conekta-android/master/refs/import.png)
    
3. Update the `manifest.xml` of your application and add next lines:

	``` java
	<uses-permission android:name="android.permission.INTERNET" />
	
	<application ...>
	...
        	<meta-data android:name="conektakey" android:value="YOUR_CONEKTAKEY" />
	...
	</application>
	
	
## Usage 
#### 1. `Simple Charge`
``` java
	Address address = new Address("250 Alexis St", "Red Deer", "Alberta", "Canada", "T4N 0B8");
	BigInteger numberCard = new BigInteger("4111111111111111");
	Card card = new Card(numberCard, 12, 2015, "Thomas Logan", 666);
	card.setAddress(address);
	BigInteger amount = new BigInteger("20000");
	ChargeCard chargeCard = new ChargeCard(card, "Charge from android", amount, Currency.MXN);
	chargeCard.setReferenceId("9893-cohib_s1_wolf_pack");
	Conekta.charge(this, chargeCard, new JsonHttpResponseHandler() {
	
		@Override
		public void onSuccess(JSONObject jsono) {}
		
		@Override
		public void onFailure(Throwable thrwbl, JSONObject jsono) {}
	});
```
        
#### 2. `OXXO Charge`
``` java
	BigInteger amount = new BigInteger("20000");
	Cash cash = new Cash(CashType.OXXO);
	ChargeCash chargeCash = new ChargeCash(cash, "Charge from android", amount, Currency.MXN);
	chargeCash.setReferenceId("9893-cohib_s1_wolf_pack");
	Details details = new Details("Wolverine", "403-342-0642", "logan@x-men.org");
	chargeCash.setDetails(details);
	Conekta.charge(this, chargeCash, new JsonHttpResponseHandler() {
	
		@Override
		public void onSuccess(JSONObject jsono) {}
		
		@Override
		public void onFailure(Throwable thrwbl, JSONObject jsono) {}
	});
```        
#### 3. `Bank Charge`
``` java
	Bank bank = new Bank(BankType.BANORTE);
	BigInteger amount = new BigInteger("20000");
	ChargeBank chargeBank = new ChargeBank(bank, "Charge from android", amount, Currency.MXN);
	chargeBank.setReferenceId("9893-cohib_s1_wolf_pack");
	Details details = new Details("Wolverine", "403-342-0642", "logan@x-men.org");
	chargeBank.setDetails(details);
	Conekta.charge(this, chargeBank, new JsonHttpResponseHandler() {
	
		@Override
		public void onSuccess(JSONObject jsono) {}
		
		@Override
		public void onFailure(Throwable thrwbl, JSONObject jsono) {}
	});
```
	
