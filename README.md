# Bytte-Mobile-ANDROID-SDK-NATIVE

<p align="center" >
  <img src="https://www.bytte.com.co/ftpaccess/Varios/CarlosG/ImgDocumentation/logo.png" alt="bytte" title="bytte">
</p>

# Bytte SDK Android

## Actualizacion bytte 14 noviembre 2023

### Captura de documentos

Soporte de captura de documentos cédula de ciudadanía de hologramas, digital componente físico, cédula de extranjería, pasaporte, pasaporte con extracción NFC.
se deprecia la captura en formato imagen jpg en las capturas, se recomienda el metodo de imgpback el cual garantiza temas de seguridad.

## Integración sdk Bytte Android

    Autor Venancio prada.
    Fecha de creación 9 septiembre 2021.
    versión  documentación -> 2.0.0.

# CONFIDENCIALIDAD

La información contenida en el presente documento es CONFIDENCIAL, hace parte del secreto comercial e industrial de la empresa e implica transmisión de información cuya propiedad corresponde exclusivamente a BYTTE SAS. En consecuencia, la divulgación o el uso inapropiado de la información aquí contenida por parte del receptor de la misma, implicarán la aplicación de las normas legales pertinentes para su debida protección.

# Factores Limitantes

Los factores limitantes para la integración del SDK son:

- Se debe verificar la calidad de la cámara, es recomendable utilizar dispositivos con cámara que tengan la característica de “AutoFoco” y flash.
- Se recomiendan cámaras con resolución mayores o iguales a 5 MegaPixeles frontal y 8 MegaPixeles para un óptimo rendimiento, “mejor cámara mejora las imágenes”.
- El SDK no funciona sobre dispositivos virtuales, únicamente sobre dispositivos físicos.
- No presenta inconveniente para compilaciones Android 33.
- Mínima versión soportada Android 23.
- Esta solución ya trabaja sobre androidX por lo cual si el proyecto no lo soporta se debe migrar para que la captura de los documentos funcionen.

- **Se debe verificar la calidad de la cámara, es recomendable utilizar dispositivos con cámara que tengan la característica de “Auto Foco” habilitada.**
- **Se recomiendan cámaras con resolución mayores o iguales a 8 MegaPixeles para un óptimo rendimiento.**
- **Sistemas soportados Android 6.0 nivel de api 23. arquitecturas arm 32,64 bits.**

# Instalación de las librerías

En el archivo gradle build.gradle del proyecto adicionaremos la 'URL' que nos entrega Bytte para la descarga de los archivos necesarios, al igual que el usuario y token de acceso.

> Las librerías tiene soporte tanto a 32 como a 64 bit en arm.

> Credenciales provistos por bytte para la syncronizacion de las librerias.

> - Url

> - name

> - username

> - password

```gradle

android{
    defaultconfig  después de
    versionName ingresamos
    ndk {abiFilters  "armeabi-v7a", "arm64-v8a"}


repositories {
        maven {
        url 'https://byttetfs.pkgs.visualstudio.com/BytteSDKLibrarys-Android/_packaging/SdkBytteV2/maven/v1'
        name 'SdkBytteV2'
            credentials {
                username ""
                password ""
            }
        }
    maven { url "https://raw.githubusercontent.com/iProov/android/master/maven/" }
}
```

# Importamos las Librerias Bytte

En el archivo gradle _build.gradle_ adicionaremos las dependencias.

> Estas son las librerías necesarias para el uso, funcionalidad y captura de documento colombiano, y biometría.

## Dependencias buid.gradle

```gradle



    implementation 'com.squareup.okhttp3:okhttp:4.9.1'
    implementation("com.squareup.okhttp3:logging-interceptor:4.9.0")
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
    implementation 'com.jakewharton.timber:timber:4.7.1'
    implementation 'com.jakewharton.retrofit:retrofit2-kotlin-coroutines-adapter:0.9.2'

    implementation 'androidx.appcompat:appcompat:1.4.1'
    implementation 'androidx.legacy:legacy-support-v4:1.0.0'

    implementation 'org.jetbrains.kotlin:kotlin-stdlib:1.6.10'
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-core:1.5.0'
    implementation 'org.jetbrains.kotlin:kotlin-android-extensions-runtime:1.6.10'


    implementation 'com.android.volley:volley:1.2.1'

    implementation "androidx.exifinterface:exifinterface:1.3.3"
    implementation 'com.google.android.gms:play-services-vision:20.1.3'

    implementation "androidx.core:core-ktx:1.6.0"
    implementation 'androidx.lifecycle:lifecycle-viewmodel-ktx:2.4.0'
    implementation 'androidx.lifecycle:lifecycle-livedata-ktx:2.4.0'


    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.5.0'
    implementation "com.google.android.material:material:1.5.0"
    implementation 'androidx.constraintlayout:constraintlayout:2.1.3'
    implementation 'com.android.support.constraint:constraint-layout:2.0.4'

    implementation 'com.bytte.microblink:LibBlinkIDCustom:5.20.0'
    implementation 'com.document.bytte:documentBytte:9.1.2'


    implementation 'com.google.mlkit:face-detection:16.1.5'

    implementation 'com.bytte.biometric:BytteFinger:8.2.1'
    implementation 'com.bytte.indenty:finger:5.7.3'



    implementation(group: 'com.bytte.biometric', name: 'FingerFace', version: '8.3.0.005-Up')
    implementation(group: 'com.bytte.indenty', name: 'face', version: '4.8.1')



    implementation 'com.iproov.sdk:iproov:9.0.0'
    implementation group: "com.iproov.android-api-client", name: "kotlin-fuel", version: "2.0.1"
    implementation group: "com.iproov.android-api-client", name: "kotlin-common", version: "2.0.1"
    implementation "org.jetbrains.kotlinx:kotlinx-coroutines-jdk8:1.2.1"
    implementation "androidx.lifecycle:lifecycle-runtime-ktx:2.4.1"
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"





```

## Manifest

> La configuración del manifest es la siguiente: requiere permisos para el uso de internet, lectura y escritura en el dispositivo y cámara.
> Configuración de las actividades Bytte para las capturas.

```
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

 <uses-feature
        android:name="android.hardware.camera"
        android:required="true" />






```

## Captura de Insumos

El app debe solicitar los permisos en tiempo de ejecución antes de usar la funcionalidad y validar que el permiso fue otorgado.

## Para las capturas es necesario la siguiente parametrizacion

las imagenes en jpg o png estan depreciadas para la implementacion.

- **setkey -> true: las imagenes van protejidas**
- **setKeyjoin -> true : todas las imagenes estan en un unico archivo.**
- **setImgpback -> true : solo se retorna un identificador por la captura.**

## Captura Documento

### Inicializar la captura.

> Activity :Pasamos
> new InitializationListener<IDCaptureDocumentBytte>() :establecer los parámetros de configuración del SDK deseados, en el método onInit().
> new BytteResponseListener<String>() :callbacks donde llegara la respuesta correcta "onResponse" o errónea "onErrorResponse"

```kotlin
  IDCaptureDocumentBytte.newInstance(Activity(), new InitializationListener<IDCaptureDocumentBytte>() {
        @Override
        public void onInit(IDCaptureDocumentBytte d) {
            d.seturl(url);
            d.setkeyProtect(key);
            d.setbytteProtect(true);
            d.setKeyjoin(true);
            d.setColorimg(false)
            d.setdocumenttype(ETipoDocumento.)
            d.setcapturetype(ETipocaptura.);
            d.settimeOut(timeOut);
            d.setcountry()
            d.capture();
            }
        }, new BytteResponseListener<String>() {
            @Override
            public void onResponse(String results) {

            }

            @Override
            public void onErrorResponse(String obj) {

            }
        });
```

### Configuración Parámetros la captura.

onInit(IDCaptureDocumentBytte d)

| Parametro                                 | Tipo de dato  | Descripcion                                                                                                                                                                                         |
| ----------------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| d.seturl(url)                             | String        | url Provisto por bytte para la inicialización en la captura de documentos parámetro requerido para su funcionamiento.                                                                               |
| setImgColor                               | Boolean       | Identifica si la img está a color o blanco y negro 'en android esto puede ser muy restrictivo por lo cual se recomienda setearlo en false'                                                          |
| d.setTimeOut(timeOut)                     | Boolean       | Tiempo de duración de la captura                                                                                                                                                                    |
| d.setcapturetype(ETypecapture.BACK)       | ETypecapture  | Identifica la captura a generarse ETypecapture.BACK -> reverso, ETypecapture.FRONT -> frontal.                                                                                                      |
| d.setkeyProtect(key);                     | String        |                                                                                                                                                                                                     |
| d.setbytteProtect(true);                  | Boolean       | Variable por defecto en True. Esta variable retorna un KEY de imagen (No retorna imagenes)                                                                                                          |
| d.setKeyjoin(true);                       | Boolean       | Las imagenes capturadas las retorna en un unico archivo.                                                                                                                                            |
| d.setdocumenttype(ETypeDocument.DOCUMENT) | ETypeDocument | DOCUMENT -> Documentos de identidad : identifica la captura segun el country , PASPORTDOCUMENT -> Pasaporte : cuando se selecciona no tiene encuenta en country , CREDITCARD -> Tarjeta de credito. |
| d.setCountry(Country.CO)                  | Country       | dentifica el pais y versión del documento CO -> Documento colombiano Hologramas COV2 -> Documento colombiano Digital COCET2 -> Documento colombiano extrangeria.                                    |
|                                           |               |

### Respuesta Captura Documentos:

                                                                           |

### Respuesta Cédula Hologramas Reverso:

| Campo            | Tipo    |
| ---------------- | ------- |
| BarcodeBase64    | String  |
| CiudadExpedicion | String  |
| CiudadNacimiento | String  |
| CodigoOperacion  | String  |
| DepartamentoCol  | String  |
| FechaExp         | String  |
| FechaNacimiento  | String  |
| MensajeOriginal  | String  |
| MensajeRetorno   | String  |
| NombresCompletos | String  |
| NumeroCedula     | String  |
| NumeroTarjeta    | String  |
| Pais             | String  |
| PathImagen       | String  |
| PrimerApellido   | String  |
| PrimerNombre     | String  |
| RH               | String  |
| SegundoApellido  | String  |
| SegundoNombre    | String  |
| Sexo             | String  |
| StatusOperacion  | Boolean |
| TipoDedo         | String  |
| TipoDedo2        | String  |
| VersionCedula    | String  |

### Respuesta Cédula Hologramas Frente:

| Campo            | Tipo    |
| ---------------- | ------- |
| Apellidos        | String  |
| CodigoOperacion  | String  |
| MensajeOriginal  | String  |
| MensajeRetorno   | String  |
| Nombres          | String  |
| NumeroCedula     | String  |
| PathImagen       | String  |
| PathImagenFull   | String  |
| PathImagenRostro | String  |
| StatusOperacion  | Boolean |

### Respuesta Cédula Digital Reverso:

| Campo              | Valor   |
| ------------------ | ------- |
| CodigoOperacion    | String  |
| MensajeOriginal    | String  |
| MensajeRetorno     | String  |
| StatusOperacion    | Boolean |
| ReversoMRZ         |         |
| - PathImagen       | String  |
| - Apellidos        | String  |
| - CodigoDocumento  | String  |
| - Edad             | String  |
| - Emisor           | String  |
| - FechaExpiracion  | String  |
| - FechaNacimiento  | String  |
| - MRZ              | String  |
| - Nacionalidad     | String  |
| - Nombres          | String  |
| - NombresCompletos | String  |
| - NumeroDocumento  | String  |
| - OPT              | String  |
| - RUN              | String  |
| - Sexo             | String  |
| - TipoDocumento    | String  |
| - Version1         | String  |

### Respuesta Cédula Digital Frente:

| Campo              | Valor   |
| ------------------ | ------- |
| MensajeOriginal    | String  |
| MensajeRetorno     | String  |
| StatusOperacion    | Boolean |
| CodigoOperacion    | String  |
| Frente             |         |
| - PathImagen       | String  |
| - PathImagenFull   | String  |
| - PathImagenRostro | String  |
| - Nombres          | String  |
| - NumeroCedula     | String  |

### Respuesta Cédula Extranjería Reverso:

| Campo              | Valor   |
| ------------------ | ------- |
| CodigoOperacion    | String  |
| MensajeOriginal    | String  |
| MensajeRetorno     | String  |
| StatusOperacion    | Boolean |
| ReversoMRZ         |         |
| - PathImagen       | String  |
| - Apellidos        | String  |
| - CodigoDocumento  | String  |
| - Edad             | String  |
| - Emisor           | String  |
| - FechaExpiracion  | String  |
| - FechaNacimiento  | String  |
| - MRZ              | String  |
| - Nacionalidad     | String  |
| - Nombres          | String  |
| - NombresCompletos | String  |
| - NumeroDocumento  | String  |
| - OPT              | String  |
| - RUN              | String  |
| - Sexo             | String  |
| - TipoDocumento    | String  |
| - Version1         | String  |

### 3.3.2.6 Respuesta Cédula Extranjería Frente:

| Campo              | Valor   |
| ------------------ | ------- |
| CodigoOperacion    | String  |
| MensajeOriginal    | String  |
| MensajeRetorno     | String  |
| StatusOperacion    | Boolean |
| Frente             |         |
| - PathImagen       | String  |
| - PathImagenFull   | String  |
| - PathImagenRostro | String  |
| - FechaExpiracion  | String  |
| - NumeroCedula     | String  |
| - IsExpired        | Boolean |

### Respuesta Pasaporte:

| Campo                | Valor   |
| -------------------- | ------- |
| Apellidos            | String  |
| Codigo               | String  |
| CodigoOperacion      | String  |
| Emisor               | String  |
| FechaExpiracion      | String  |
| FechaNacimiento      | String  |
| IdTipoDocumento      | String  |
| IdentificadorProceso | String  |
| MRZ                  | String  |
| Nacionalidad         | String  |
| Nombres              | String  |
| NumeroDocumento      | String  |
| NumeroPersonal       | String  |
| Opt2                 | String  |
| PathImagen           | String  |
| Sexo                 | String  |
| StatusOperacion      | Boolean |
| Version1             | String  |
| IsExpired            | Boolean |

## Captura Biometria

## Licenciamiento Biometría Huellas y Rostro Facial ID

## Licencia Android para el uso de huellas

- **Crear una carpeta en el directorio android llamada 'assets'.**
  Dentro de esa carpeta depositamos el archivo de licencia que se genera para la implementación en 'debug' y otra, reléase.

## Captura Biometría huellas

### Parámetros

```kotlin

        ResponseIDBiometric callback = new ResponseIDBiometric() {
            @Override
            public void objBiometricResoult(IDBiometricResult result) {

            }
        };

        IDCaptureBiometric idfinger = new IDCaptureBiometric(namePath, "", callback, reactContext.getCurrentActivity());
        idfinger.captureInitFaceprint("url","key",fingernumber,timeout,keyjoin);

```

### Configuración Parámetros:

| Parametro    | Tipo de dato | Descripcion                                                                                                                                                                     |
| ------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| url          | String       | URL proporcionada por Bytte para la captura dactilar.                                                                                                                           |
| bytteProtect | Boolean      | Variable por defecto en **_True_**. Esta variable retorna un KEY de imagen (No retorna imagenes)                                                                                |
| keyProtect   | String       | Llave de protección para las imagenes. Si lleva un valor diferente a vacío esta retorna la imagen en formato .bytte, el resultado es una imagen cifrada con aes 256 por sesión. |
| keyJoin      | Boolean      | Las imagenes capturadas las retorna en un unico archivo.                                                                                                                        |
| timeOut      | Int          | Tiempo de duración de la captura.                                                                                                                                               |
| fingerNumber | Int          | Variable dedo a capturar **_2_** -> Mano derecha. **_7_** -> Mano Izquierda.                                                                                                    |

## Configuración colores de la pantalla de huellas

> boxes -> Color de borde del cuadro de la cámara.
> boxes_transparent -> Color del recuadro entre el header y el footer.
> colorPrimary -> Color del footer y el header.

    ```  xml
    <color name="boxes">#FF5722</color>
    <color name="boxes_transparent">#FF5722</color>
    <color name="colorPrimary">#FFC107</color>
    <color name="colorPrimaryDark">#FF5722</color>

    ```

## Configuración en español para mensajes huellas

Vamos a la carpeta res/values/strings.xml

```xml
 <string name="id_searching_left">Buscando dedos izquierdos…</string>
    <string name="id_searching_right">Buscando dedos derechos…</string>




        <string name="id_authentication_retake">INSEGURO VOLVER A TOMAR</string>
        <string name="id_authentication_successful">Autenticado</string>
        <string name="id_authentication_unsuccessful">Autenticación incorrecta</string>
        <string name="id_capture_completed">Captura completada</string>
        <string name="id_captured">Capturado</string>
        <string name="id_capturing">Capturando..</string>
        <string name="id_close">Cerrar</string>
        <string name="id_confirm_exit">Confirmar salida</string>
        <string name="id_continue">SEGUIR</string>
        <string name="id_dshow_again">No me lo muestres de nuevo</string>
        <string name="id_enrollment_completed">INSCRIPCIÓN FINALIZADA</string>
        <string name="id_exit_text">¿Quieres salir de la captura?</string>
        <string name="id_good_quality">Todo de buena calidad</string>
        <string name="id_hand_closer">Por favor acerca la mano</string>
        <string name="id_hand_further_away">Mueva la mano más lejos</string>
        <string name="id_hand_further_away_ff">Mueva la mano más lejos 4F</string>
        <string name="id_hold_0">Por favor sostenga</string>
        <string name="id_hold_1">Por favor sostenga 1</string>
        <string name="id_hold_2">Por favor sostenga 2</string>
        <string name="id_hold_3">Por favor sostenga 3</string>
        <string name="id_hold_4">Por favor sostenga 4</string>
        <string name="id_hold_5">Por favor sostenga 5</string>
        <string name="id_hold_6">Por favor sostenga 6</string>
        <string name="id_hold_still">Asegúrate de mantenerte quieto hasta la captura automática. </string>
        <string name="id_identy_template_format">Formato de plantilla IDENTY</string>
        <string name="id_image_cd_todo">QUE HACER</string>
        <string name="id_in_front_camera">2.Coloque los dedos frente a la cámara</string>
        <string name="id_index">INDICE    </string>
        <string name="id_index_finger">dedo índice</string>
        <string name="id_inside_guide">Por favor, esté dentro de la guía.</string>
        <string name="id_keep_fingers">1.Extiende y mantén los dedos juntos</string>
        <string name="id_keep_fingers_together">mantener los dedos juntos</string>
        <string name="id_left_thumb"> PULGAR IZQUIERDO</string>
        <string name="id_little">PEQUEÑO   </string>
        <string name="id_little_finger">dedo índice</string>
        <string name="id_location_error_off">Algo es extraño APAGADO</string>
        <string name="id_middle">MEDIO   </string>
        <string name="id_middle_finger">dedo medio</string>
        <string name="id_next">SIGUIENTE</string>
        <string name="id_next_detection">Pasar a la siguiente mano ?</string>
        <string name="id_next_hand_confirm">Siguiente detección Confirmar</string>
        <string name="id_no">NO</string>
        <string name="id_no_match">SIN COINCIDENCIA</string>
        <string name="id_not_good_quality">no tiene buena calidad.</string>
        <string name="id_ok">OK</string>
        <string name="id_pic_qc_title">FALLO EN LA CALIDAD DE LA IMAGEN</string>
        <string name="id_processing">Procesando …</string>
        <string name="id_qc_retake">Necesitamos retomar la foto</string>
        <string name="id_quality_failed">Falló la calidad de la imagen</string>
        <string name="id_retake_additional_tip">Consejos adicionales</string>
        <string name="id_retake_match">Se alcanzó el número máximo de intentos, inténtelo de nuevo</string>
        <string name="id_retake_q">volver a tomar?</string>
        <string name="id_retake_string">volver a tomar</string>
        <string name="id_retake_tip_1">Tus dedos miran hacia la cámara</string>
        <string name="id_retake_tip_2">Tus dedos están dentro de la caja azul</string>
        <string name="id_retake_tip_3">Utilice iluminación interior normal</string>
        <string name="id_retry">Procesar de nuevo</string>
        <string name="id_right_thumb">PULGAR DERECHO</string>
        <string name="id_ring">ANILLO     </string>
        <string name="id_ring_finger">dedo anular</string>
        <string name="id_select_hand">por favor seleccione al menos una mano</string>
        <string name="id_spoof">PARODIA</string>
        <string name="id_spoof_additional_tip">Consejos adicionales</string>
        <string name="id_spoof_question">¿Estás usando manos reales para autenticarte?</string>
        <string name="id_spoof_tip_2">Utilice iluminación interior normal  </string>
        <string name="id_spoof_tip_3">Intente intentar una ubicación / fondo diferente</string>
        <string name="id_spoof_title">Spoof detectado</string>
        <string name="id_stable">Por favor sea estable</string>
        <string name="id_stay_still_blue">3.Quédate quieto dentro del rectángulo azul</string>
        <string name="id_success">Éxito</string>
        <string name="id_success_match"> MATCH EXITOSO</string>
        <string name="id_thumb">PULGAR    </string>
        <string name="id_thumb_finger">dedo índice</string>
        <string name="id_try_again">Intentar otra vez</string>
        <string name="id_try_again_in">Inténtelo de nuevo en : </string>
        <string name="id_wait_auto">4.Espere la captura automática (hasta que se apague el flash)</string>
        <string name="id_wsq_compression">Relación de compresión WSQ</string>
        <string name="id_yes">SI</string>
        <string name="id_zero">0</string>
```

## Captura Biometría facial-id

```kotlin

               IDCaptureBiometricFaceid facecallback = new IDCaptureBiometricFaceid() {
            @Override
            public void onResponse(String results) {

            }

            @Override
            public void onErrorResponse(String results) {

            }

        };

        IDCaptureBiometricFaceid.newInstance(new InitListener<IDCaptureBiometricFaceid>() {
            @Override
            public void onInit(IDCaptureBiometricFaceid d) {
                d.act=reactContext.getCurrentActivity();
                d.camera=0;
                d.bytteProtect=true
                d.license="2026-miid.appdigital.bio-31-12-2023.lic";
                d.keyProtect=keyvalue;
                d.url="https://portal.bytte.com.co/casb/SmartBio/";
                d.captureFace();
            }
        },facecallback);


```

### Configuración Parámetros:

| Parametro    | Tipo         | Descripción                                                                                                                                                                     |
| ------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| url          | String       | URL proporcionada por Bytte para la captura dactilar.                                                                                                                           |
| bytteProtect | Boolean      | Variable por defecto en **_True_**. Esta variable retorna un KEY de imagen (No retorna imagenes)                                                                                |
| keyProtect   | String       | Llave de protección para las imagenes. Si lleva un valor diferente a vacío esta retorna la imagen en formato .bytte, el resultado es una imagen cifrada con aes 256 por sesión. |
| timeOut      | Int          | Tiempo de duración de la captura.                                                                                                                                               |
| camera       | camera.Front | Indica sobre que camara inicia el sdk **_Front_** -> Camara Frontal **_Back_** -> Camara Reverso                                                                                |
| act          | activity     | instancia de la activity                                                                                                                                                        |

## Configuración colores de la pantalla de facial

### Colores para personalizar la vista

Estos colores se toman de la configuración de la app

> id_box -> Color del mensaje
> id_face_boxes -> Color del borde
> colorPrimary -> Color del footer y el header

```

    <color name="id_box">#FF5722</color>
    <color name="id_face_boxes">#8BC34A</color>
```

### 3.6. Captura Biometria Facial IP:

Para realizar el llamado de captura facial V2 es necesario inicializar y agregar variables de captura. A continuación, se presenta un ejemplo:

````kotlin

   ```kotlin

               IDCaptureBiometricFaceip facecallback = new IDCaptureBiometricFaceip() {
            @Override
            public void onResponse(String results) {

            }

            @Override
            public void onErrorResponse(String results) {

            }

        };

        IDCaptureBiometricFaceip.newInstance(new InitListener<IDCaptureBiometricFaceip>() {
            @Override
            public void onInit(IDCaptureBiometricFaceip d) {
                d.act=reactContext.getCurrentActivity();
                d.camera=0;
                d.bytteProtect=true
                d.keyProtect=keyvalue;
                d.url="https://portal.bytte.com.co/casb/SmartBio/";
                d.captureFace();
            }
        },facecallback);




````

### Configuración Parámetros:

| Parametro  | Tipo     | Descripción                                                                                                                                                                     |
| ---------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| url        | String   | URL proporcionada por Bytte para la captura dactilar.                                                                                                                           |
| keyProtect | String   | Llave de protección para las imagenes. Si lleva un valor diferente a vacío esta retorna la imagen en formato .bytte, el resultado es una imagen cifrada con aes 256 por sesión. |
| timeOut    | Int      | Tiempo de duración de la captura.                                                                                                                                               |
| camera     | Enum     | Indica sobre que camara inicia el sdk **_Front_** -> Camara Frontal **_Back_** -> Camara Reverso                                                                                |
| act        | activity | instancia de la activity                                                                                                                                                        |

# Código de errores

```
<string name="OK">0000</string><string name="TimeOut">0001</string>
<string name="Cancelado_a_proposito">0002</string>
<string name="Error_de_Licencia_MicroBlink">0111</string>
<string name="Error_No_tiene_permisos_camara">0112</string>
<string name="Error_de_Licencia_Biometria">0113</string>
<string name="Error_Captura_de_huellas">0114</string>


<string name="timeOut">TimeOut</string>
<string name="Canceladoproposito">Cancelado a proposito</string>
<string name="ErrorLicencia_MicroBlink">Error de Licencia MicroBlink"</string>
<string name="ErrorLicencia_Biometria">Error de Licencia biometría"</string>
<string name="Error_Capturahuellas">Error en la captura de las huellas"</string>
<string name="ErrorLicenciaBiometria">Error licencia de  biometría"</string>

------------------------------
Control de cambios
------------------------------

```
