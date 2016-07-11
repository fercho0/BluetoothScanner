#BuetoothScanner

[Bluetooth](https://en.wikipedia.org/wiki/Bluetooth) se ha convertido en una muy popular tecnología, especialmente en dispositivos móviles. Es una tecnología para descubrir y transferir datos entre dispositivos cercanos. Virtualmente cada dispositivo móvil moderno tiene capacidades Bluetooth éstos días. Si quieres crear una interfaz de aplicación con otro dispositivo con Bluetooth habilitado, desde teléfonos hasta altavoces, debes saber cómo usar la API de Bluetooth de Android.

En éste tutorial, crearemos una aplicación que es similar a la aplicación con Bluettoth integrado en la configuración de Android. Incluirá las siguientes características:

	- habilitar Bluetooth en un dispositivo
	- desplegar una lista de dispositivos asociados
	- descubrir y listar dispositivos Bluetooth cercanos

Iremos sobre las bases para conectar y enviar datos a otro dispositivo Bluetooth. He creado un proyecto para iniciarnos, el cual puedes descargar desde [Github](https://github.com/fercho0?tab=overview&from=2016-07-09). La captura de pantalla de abajo muestra como se ve el proyecto de inicio. Si te estancas o encuentras problemas, entonces puedes observar el proyecto finalizado en [Githb](https://github.com/fercho0/BluetoothScanner).


![alt tag](https://github.com/fercho0/BluetoothScanner/blob/master/img/b1.png)

##Habilitar Bluetooth

Antes de que podamos habilitar Bluetooth en un dispositivo Android, necesitamos requerir los permisos necesarios. Hacemos ésto en el manifiesto de la aplicación. El permiso BLUETOOTH deja que nuestra aplicación se conecte, se desconecte, y transfiera datos con otro disositivo Bluetooth. El permiso [BLUETOOTH_ADMIN](https://developer.android.com/reference/android/Manifest.permission.html) deja que nuestra aplicación descubra nuevos dispositivos Bluetooth y cambia los ajustes sobre Bluetooth del dispositivo.

<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.tutsplus.matt.bluetoothscanner" >
     
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />

Usaremos el adaptador Bluetooth para conectarse mediante interfaz con Bluetooth. Instanciamos el adaptador en la clase ListActivity. Si el adaptador es null, ésto significa que Bluetooth no es soportado por el dispositivo y la aplicación no funcionará en el dispositivo actual. Manejamos ésta situación mostrando un diálogo de alerta al usuario y saliendo de la aplicación.
´´´
@Override
protected void onCreate(Bundle savedInstanceState) {
...
    BTAdapter = BluetoothAdapter.getDefaultAdapter();
    // Phone does not support Bluetooth so let the user know and exit.
    if (BTAdapter == null) {
        new AlertDialog.Builder(this)
                .setTitle("Not compatible")
                .setMessage("Your phone does not support Bluetooth")
                .setPositiveButton("Exit", new DialogInterface.OnClickListener() {
                    public void onClick(DialogInterface dialog, int which) {
                        System.exit(0);
                    }
                })
                .setIcon(android.R.drawable.ic_dialog_alert)
                .show();
    }
}
´´´