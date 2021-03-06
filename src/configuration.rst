.. _configuration:

=============
Configuration
=============

You are need create configuration for gateway. Library supporting single or multiple gateways,
because for every currency you are need one.


.. _configuration.attributes:

Attributes
##########

.. _configuration.attributes.privateKey:

The `privateKey` attribute
--------------------------
Possible values: absolute path to your private certificate `pem` file.

Type: `string`

.. _configuration.attributes.privateKeyPassphrase:

The `privateKeyPassphrase` attribute
------------------------------------
Possible values: passphrase of your private certificate

Type: `string`

.. _configuration.attributes.publicKey:

The `publicKey` attribute
-------------------------
Possible values: absolute path to GPWebPay service public certificate `pem` file.

Type: `string`

.. _configuration.attributes.url:

The `url` attribute
-------------------
Possible values: absolute URL to gateway

Type: `string`

The address you are get from GPWebPay

.. _configuration.attributes.depositFlag:

The `depositFlag` attribute
---------------------------
Possible values: `0` or `1`

Type: `int`

Specifies if the order has to be paid for automatically.
`0` = instant payment not required `1` = payment required

.. _configuration.attributes.merchantNumber:

The `merchantNumber` attribute
------------------------------
Possible values: your Merchant Number

Type: `string`

Your Merchant number you are get from GPWebPay service.

.. _configuration.attributes.responseUrl:

The `responseUrl` attribute
---------------------------
Possible values: absolute URL to your site where GPWebPay sends a response

Type: `string`

It is optional in config. You can set up url for each request in Operation object.
By GPWebPay is recommendation does not use url which has parameters (after '?')
because they may drop it for *"security reason"*.

.. _configuration.example:

Examples
########

.. _configuration.example.single_gateway:

Single gateway
--------------

.. code-block:: php

	use Pixidos\GPWebPay\Config\Factory\ConfigFactory;
	use Pixidos\GPWebPay\Config\Factory\PaymentConfigFactory;

	$configFactory = new ConfigFactory(new PaymentConfigFactory());

	$config = $configFactory->create(
		[
			ConfigFactory::PRIVATE_KEY => __DIR__ . '/_certs/test.pem',
			ConfigFactory::PRIVATE_KEY_PASSPHRASE => '1234567',
			ConfigFactory::PUBLIC_KEY => __DIR__ . '/_certs/test-pub.pem',
			ConfigFactory::URL => 'https://test.3dsecure.gpwebpay.com/unicredit/order.do',
			ConfigFactory::MERCHANT_NUMBER => '123456789',
			ConfigFactory::DEPOSIT_FLAG => 1,
			ConfigFactory::RESPONSE_URL => 'http://example.com/proccess-gpw-response'
		]
	);


.. _configuration.example.multiple_gateways:

Multiple gateways
-----------------

.. code-block:: php

	use Pixidos\GPWebPay\Config\Factory\ConfigFactory;
	use Pixidos\GPWebPay\Config\Factory\PaymentConfigFactory;

	$configFactory = new ConfigFactory(new PaymentConfigFactory());

	$config = $configFactory->create(
		[
			'czk' => [
				ConfigFactory::PRIVATE_KEY => __DIR__ . '/_certs/test.pem',
				ConfigFactory::PRIVATE_KEY_PASSPHRASE => '1234567',
				ConfigFactory::PUBLIC_KEY => __DIR__ . '/_certs/test-pub.pem',
				ConfigFactory::URL => 'https://test.3dsecure.gpwebpay.com/unicredit/order.do',
				ConfigFactory::MERCHANT_NUMBER => '123456789',
				ConfigFactory::DEPOSIT_FLAG => 1,
			],
			'eur' => [
				ConfigFactory::PRIVATE_KEY => __DIR__ . '/_certs/test2.pem',
				ConfigFactory::PRIVATE_KEY_PASSPHRASE => '12345678',
				ConfigFactory::PUBLIC_KEY => __DIR__ . '/_certs/test-pub2.pem',
				ConfigFactory::URL => 'https://test.3dsecure.gpwebpay.com/unicredit/order.do',
				ConfigFactory::MERCHANT_NUMBER => '123456780',
				ConfigFactory::DEPOSIT_FLAG => 1,
			],
		],
		'czk' // what gateway is default
	);
