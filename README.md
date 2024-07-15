## Tentang
Halo! nama saya Louis Bryan, saya seorang developer server Minecraft yang sudah berkecimpung di-industri ini selama kurang lebih 3 tahun. Saya sudah memiliki pengalaman memberi optimisasi pada banyak jenis server dengan masalah yang berbeda-beda, tentu tidak ada optimasi server "One size fit all" tapi optimasi ini bisa membantu untuk memulai optimasi server kamu.

## Server JAR
<10 players - [Vanilla](https://www.minecraft.net/en-us/download/server/) | Minecraft software standard yang dibuat dan didistribusi oleh Mojang.

10-15 players - [Spigot](https://www.spigotmc.org/) | Menambahkan plugin! Berbasis bukkit (sekarang CraftBukkit) serta membawa beberapa optimasi

15-50 players - [Paper](https://papermc.io/) | Memberikan bug serta dupe fix pada versi vanilla. Sudah digabung dengan Tuinity untuk boost performa!

50-100 players - [Pufferfish](https://pufferfish.host/downloads) | Performa boost yang gila! Jangan gunakan jika kamu bukan server yang sangat besar dan butuh performa lebih!

50-100 players - [Purpur](https://purpurmc.org) | Dibuat berbasis dari Pufferfish, JANGAN digunakan jika kamu tidak ingin merubah vanilla feature. Tidak direkomendasi jika kamu ingin pengalaman "Vanilla"

## Penggunaan Distribusi Java
Gw merekomendasi untuk menggunakan [Adoptium](https://adoptium.net/), tidak ada memory leak yang diketahui dan sangat sering diguanakan. Untuk sekarang, gunakan Java 18 karena ada G1GC improvement daripada 17.

## Startup Command
gw mempelajari Aikar flag JVM selama beberapa minggu sebelum bikin ini. G1 garbage collector menawarkan stabilitas yang hebat dengan kinerja yang mantap, tapi mungkin lambat dalam kriteria tertentu, itu membantu server besar pada waktu itu dan masih membantu mereka saat ini, tetapi Java berevolusi. Semakin banyak garbage collector yang dibuat, dan alternatif yang baik saat ini adalah ShenandoahGC, yang secara drastis meningkatkan penggunaan CPU. Dalam waktu dekat, ZGC akan menjadi referensi garbage collector untuk server Minecraft, tetapi masih dalam pengembangan dan benar-benar mematikan CPU Anda. Itu sebabnya gw tetap menggunakan G1GC (G1 garbage collector).

***Untuk server yang menggunakan ram 12GB kebawah:***
```java
java -Xms12G -Xmx12G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -XX:-UseBiasedLocking -XX:UseAVX=3 -XX:+UseStringDeduplication -XX:+UseFastUnorderedTimeStamps -XX:+UseAES -XX:+UseAESIntrinsics -XX:UseSSE=4 -XX:+UseFMA -XX:AllocatePrefetchStyle=1 -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+UseCodeCacheFlushing -XX:+SegmentedCodeCache -XX:+UseFastJNIAccessors -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+TrustFinalNonStaticFields -XX:ThreadPriorityPolicy=1 -XX:+UseInlineCaches -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -Dfile.encoding=UTF-8 -Xlog:async -Djava.security.egd=file:/dev/urandom --add-modules jdk.incubator.vector -jar server.jar nogui
```

***Untuk server yang menggunakan ram 12GB keatas:***
```java
java -Xms20G -Xmx20G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+UnlockDiagnosticVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=40 -XX:G1MaxNewSizePercent=50 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=15 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=20 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -XX:-UseBiasedLocking -XX:UseAVX=3 -XX:+UseStringDeduplication -XX:+UseFastUnorderedTimeStamps -XX:+UseAES -XX:+UseAESIntrinsics -XX:UseSSE=4 -XX:+UseFMA -XX:AllocatePrefetchStyle=1 -XX:+UseLoopPredicate -XX:+RangeCheckElimination -XX:+EliminateLocks -XX:+DoEscapeAnalysis -XX:+UseCodeCacheFlushing -XX:+SegmentedCodeCache -XX:+UseFastJNIAccessors -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+UseThreadPriorities -XX:+OmitStackTraceInFastThrow -XX:+TrustFinalNonStaticFields -XX:ThreadPriorityPolicy=1 -XX:+UseInlineCaches -XX:+RewriteBytecodes -XX:+RewriteFrequentPairs -XX:+UseNUMA -XX:-DontCompileHugeMethods -XX:+UseFPUForSpilling -XX:+UseFastStosb -XX:+UseNewLongLShift -XX:+UseVectorCmov -XX:+UseXMMForArrayCopy -XX:+UseXmmI2D -XX:+UseXmmI2F -XX:+UseXmmLoadAndClearUpper -XX:+UseXmmRegToRegMoveAll -Dfile.encoding=UTF-8 -Xlog:async -Djava.security.egd=file:/dev/urandom --add-modules jdk.incubator.vector -jar server.jar nogui
```

Berikan headroom sebesar 1.5GB - 3GB, Contoh: jika kamu memiliki Ram 16GB maka gunakan Xms dan Xmx sebesar 13GB - 14.5GB

## Optimasi Config
Saya sudah memberi contoh file pada resp ini, kalian bisa gunakan ini sebagai contoh. Tidak disarankan untuk copy paste kecuali kalau memang kalian menggunakan versi paper yang sama.

