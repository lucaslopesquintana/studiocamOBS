# Perfil de hardware — Motorola moto g35 5G

## 1. Dados publicados pelo fabricante

Conforme especificações oficiais Motorola consultadas em 23/11/2026:

- Sistema operacional de lançamento: Android 14.
- Processador: Unisoc T760.
- Memória: variante publicada com 4 GB RAM e RAM Boost; confirmar variante local.
- Tela: FHD+ 2400×1080.
- Bateria: 5000 mAh.
- Wi-Fi: 802.11 a/b/g/n/ac, 2,4 GHz e 5 GHz.
- USB-C: USB 2.0 conforme ficha regional.
- Câmeras traseiras: principal 50 MP e ultrawide 8 MP.
- Câmera frontal: 16 MP.
- A ficha regional brasileira menciona gravação de vídeo 4K para câmera principal e Full HD 30 FPS para frontal; validar no aparelho e não inferir que Camera2/MediaCodec exponham todos os modos para streaming.

Fonte: https://pt-br.support.motorola.com/app/answers/detail/a_id/184470  
Ficha brasileira: https://www.motorola.com.br/smartphone-moto-g35-5g-256gb/p?idsku=1613

## 2. Implicações para o projeto

1. O primeiro perfil a testar deve ser 1080p30.
2. Não presumir 4K60.
3. Testar separadamente câmera principal, ultrawide e frontal.
4. Confirmar se as câmeras são expostas como IDs independentes, câmera lógica ou combinação variável.
5. Verificar encoder H.264 por hardware e os perfis suportados.
6. Monitorar aquecimento e consumo em sessões prolongadas.
7. Wi-Fi 5 GHz será preferido quando disponível; 2,4 GHz será testado como cenário de compatibilidade.
8. USB 2.0 limita a expectativa de um modo de vídeo bruto por cabo; ADB forwarding é apenas um túnel de desenvolvimento inicial.

## 3. Inventário que ainda precisa ser executado

Este arquivo não substitui inspeção do aparelho. Registrar:
- modelo/SKU e build exatos;
- versão Android e patch de segurança;
- `adb shell getprop ro.product.model`;
- `adb shell getprop ro.build.version.release`;
- `adb shell getprop ro.build.version.sdk`;
- saída de Camera2/CameraCharacteristics;
- codecs e perfis MediaCodec;
- modos de vídeo realmente aceitos;
- temperatura e desempenho em teste prolongado.

## 4. Comandos de diagnóstico inicial

```bash
adb devices
adb shell getprop ro.product.model
adb shell getprop ro.build.version.release
adb shell getprop ro.build.version.sdk
adb shell dumpsys media.camera
adb shell dumpsys media.codec
```

A saída pode variar por versão do Android e permissões. Não publicar logs integrais sem remover identificadores e dados pessoais.
