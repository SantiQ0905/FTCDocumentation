# EasyOpenCV - Computer Vision

## ¿Qué es EasyOpenCV?

Framework simplificado para usar OpenCV en FTC. Permite crear pipelines de visión por computadora personalizados.

## Instalación

```gradle
dependencies {
    implementation 'org.openftc:easyopencv:1.7.0'
}
```

## Ejemplo Básico

```java
import org.openftc.easyopencv.OpenCvCamera;
import org.openftc.easyopencv.OpenCvCameraFactory;
import org.openftc.easyopencv.OpenCvPipeline;

OpenCvCamera camera = OpenCvCameraFactory.getInstance()
    .createWebcam(hardwareMap.get(WebcamName.class, "Webcam 1"));

camera.openCameraDeviceAsync(new OpenCvCamera.AsyncCameraOpenListener() {
    @Override
    public void onOpened() {
        camera.startStreaming(320, 240, OpenCvCameraRotation.UPRIGHT);
    }
});
```

## Recursos

- **GitHub**: https://github.com/OpenFTC/EasyOpenCV
- **EOCV-Sim**: Simulador para desarrollar pipelines

---

**[↑ Índice](../INTRO_INDICE.md)**
