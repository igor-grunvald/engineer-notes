# Вопросы по Java I/O и NIO (с ответами)

## Оглавление

- [1. Основы Java I/O (Streams, Readers/Writers)](#1-основы-java-io-streams-readerswriters)
  - [1.1. Что такое потоки (Stream) в Java I/O?](#11-что-такое-потоки-stream-в-java-io)
  - [1.2. Какие основные классы есть в java.io (InputStream, OutputStream, Reader, Writer)?](#12-какие-основные-классы-есть-в-javaio-inputstream-outputstream-reader-writer)
  - [1.3. В чем разница между байтовыми (InputStream/OutputStream) и символьными (Reader/Writer) потоками?](#13-в-чем-разница-между-байтовыми-inputstreamoutputstream-и-символьными-readerwriter-потоками)
  - [1.4. Какой поток использовать для чтения текстовых файлов? А для бинарных?](#14-какой-поток-использовать-для-чтения-текстовых-файлов-а-для-бинарных)
  - [1.5. Как работает try-with-resources и почему это важно для I/O?](#15-как-работает-try-with-resources-и-почему-это-важно-для-io)
  - [1.6. Что такое паттерн Декоратор в java.io? Как он реализован?](#16-что-такое-паттерн-декоратор-в-javaio-как-он-реализован)
  - [1.7. Как работают mark() и reset()? Какие потоки их поддерживают?](#17-как-работают-mark-и-reset-какие-потоки-их-поддерживают)
  - [1.8. Что дают методы InputStream.readAllBytes() и transferTo() (Java 9+)?](#18-что-дают-методы-inputstreamreadallbytes-и-transferto-java-9)
  - [1.9. Что такое интерфейсы Flushable и Closeable?](#19-что-такое-интерфейсы-flushable-и-closeable)
- [2. Кодировки, Charset и мосты байты↔символы](#2-кодировки-charset-и-мосты-байтысимволы)
  - [2.1. Что такое Charset и как Java работает с кодировками?](#21-что-такое-charset-и-как-java-работает-с-кодировками)
  - [2.2. Что такое CharsetEncoder и CharsetDecoder? Зачем они нужны?](#22-что-такое-charsetencoder-и-charsetdecoder-зачем-они-нужны)
  - [2.3. Как работает InputStreamReader / OutputStreamWriter — мост байты↔символы?](#23-как-работает-inputstreamreader--outputstreamwriter--мост-байтысимволы)
  - [2.4. Что такое BOM (Byte Order Mark) и как его обрабатывать?](#24-что-такое-bom-byte-order-mark-и-как-его-обрабатывать)
  - [2.5. Как определить кодировку текстового файла?](#25-как-определить-кодировку-текстового-файла)
  - [2.6. Какие проблемы возникают с платформенной кодировкой по умолчанию?](#26-какие-проблемы-возникают-с-платформенной-кодировкой-по-умолчанию)
- [3. Работа с файлами (File, Path, Files, NIO.2)](#3-работа-с-файлами-file-path-files-nio2)
  - [3.1. Чем java.io.File отличается от java.nio.file.Path (Java 7+)?](#31-чем-javaiofile-отличается-от-javaniofilepath-java-7)
  - [3.2. Как прочитать файл в строку (String) с помощью Files?](#32-как-прочитать-файл-в-строку-string-с-помощью-files)
  - [3.3. Как записать данные в файл с помощью Files?](#33-как-записать-данные-в-файл-с-помощью-files)
  - [3.4. Как скопировать / переместить файл стандартными средствами Java?](#34-как-скопировать--переместить-файл-стандартными-средствами-java)
  - [3.5. Как рекурсивно обойти все файлы в директории?](#35-как-рекурсивно-обойти-все-файлы-в-директории)
  - [3.6. Как получить список файлов только текущей директории (не рекурсивно)?](#36-как-получить-список-файлов-только-текущей-директории-не-рекурсивно)
  - [3.7. Как проверить, существует ли файл?](#37-как-проверить-существует-ли-файл)
  - [3.8. Как создать временный файл?](#38-как-создать-временный-файл)
  - [3.9. Как рекурсивно скопировать/удалить папку с NIO.2?](#39-как-рекурсивно-скопироватьудалить-папку-с-nio2)
  - [3.10. Как мониторить изменения в файловой системе (WatchService)?](#310-как-мониторить-изменения-в-файловой-системе-watchservice)
  - [3.11. Как защититься от Path Traversal атак при работе с файлами?](#311-как-защититься-от-path-traversal-атак-при-работе-с-файлами)
  - [3.12. Какие StandardOpenOption бывают и зачем они нужны?](#312-какие-standardopenoption-бывают-и-зачем-они-нужны)
  - [3.13. Как Files.readString() и Files.writeString() упрощают работу с текстом (Java 11+)?](#313-как-filesreadstring-и-fileswritestring-упрощают-работу-с-текстом-java-11)
  - [3.14. Какой метод выбросит IOException при работе с Files.readAllLines()?](#314-какой-метод-выбросит-ioexception-при-работе-с-filesreadalllines)
  - [3.15. Что произойдёт, если вызвать Files.delete() для несуществующего файла?](#315-что-произойдёт-если-вызвать-filesdelete-для-несуществующего-файла)
  - [3.16. Как работает Files.mismatch() (Java 12+) и зачем он нужен?](#316-как-работает-filesmismatch-java-12-и-зачем-он-нужен)
- [4. Атрибуты файлов и метаданные файловой системы](#4-атрибуты-файлов-и-метаданные-файловой-системы)
  - [4.1. Как читать атрибуты файла: BasicFileAttributes, DosFileAttributes, PosixFileAttributes?](#41-как-читать-атрибуты-файла-basicfileattributes-dosfileattributes-posixfileattributes)
  - [4.2. Как прочитать отдельные атрибуты через Files.readAttributes()?](#42-как-прочитать-отдельные-атрибуты-через-filesreadattributes)
  - [4.3. Как получить информацию о файловой системе через FileStore?](#43-как-получить-информацию-о-файловой-системе-через-filestore)
  - [4.4. Как работать с владельцами файлов и правами доступа?](#44-как-работать-с-владельцами-файлов-и-правами-доступа)
  - [4.5. Что такое PathMatcher и как фильтровать файлы по glob/regex?](#45-что-такое-pathmatcher-и-как-фильтровать-файлы-по-globregex)
  - [4.6. Как монтировать ZIP/JAR как файловую систему через FileSystems.newFileSystem()?](#46-как-монтировать-zipjar-как-файловую-систему-через-filesystemsnewfilesystem)
- [5. Буферизация и производительность](#5-буферизация-и-производительность)
  - [5.1. Что такое буферизация (BufferedReader, BufferedInputStream)? Зачем она нужна?](#51-что-такое-буферизация-bufferedreader-bufferedinputstream-зачем-она-нужна)
  - [5.2. Почему BufferedReader эффективнее FileReader?](#52-почему-bufferedreader-эффективнее-filereader)
  - [5.3. Как работает BufferedInputStream и какой размер буфера оптимален?](#53-как-работает-bufferedinputstream-и-какой-размер-буфера-оптимален)
  - [5.4. Как прочитать большой файл (1 ГБ+) без OutOfMemoryError?](#54-как-прочитать-большой-файл-1-гб-без-outofmemoryerror)
  - [5.5. Математика буферизации: сколько системных вызовов экономится?](#55-математика-буферизации-сколько-системных-вызовов-экономится)
- [6. Байтовые массивы и специализированные потоки](#6-байтовые-массивы-и-специализированные-потоки)
  - [6.1. Что такое ByteArrayInputStream и ByteArrayOutputStream?](#61-что-такое-bytearrayinputstream-и-bytearrayoutputstream)
  - [6.2. Что такое DataInputStream и DataOutputStream?](#62-что-такое-datainputstream-и-dataoutputstream)
  - [6.3. Что такое PrintWriter и PrintStream?](#63-что-такое-printwriter-и-printstream)
  - [6.4. Что такое PipedInputStream / PipedOutputStream?](#64-что-такое-pipedinputstream--pipedoutputstream)
  - [6.5. Как работать с System.in, System.out, System.err?](#65-как-работать-с-systemin-systemout-systemerr)
  - [6.6. Что такое PushbackInputStream / PushbackReader и зачем они нужны?](#66-что-такое-pushbackinputstream--pushbackreader-и-зачем-они-нужны)
  - [6.7. Что такое SequenceInputStream и как объединить несколько потоков?](#67-что-такое-sequenceinputstream-и-как-объединить-несколько-потоков)
  - [6.8. Что такое StringReader / StringWriter и CharArrayReader / CharArrayWriter?](#68-что-такое-stringreader--stringwriter-и-chararrayreader--chararraywriter)
  - [6.9. Как работает Console (System.console()) для защищённого ввода?](#69-как-работает-console-systemconsole-для-защищённого-ввода)
  - [6.10. Что такое LineNumberReader и как отслеживать номера строк?](#610-что-такое-linenumberreader-и-как-отслеживать-номера-строк)
- [7. FileChannel и Memory Mapping](#7-filechannel-и-memory-mapping)
  - [7.1. Что такое FileChannel? Какие возможности даёт?](#71-что-такое-filechannel-какие-возможности-даёт)
  - [7.2. Как FileChannel ускоряет работу с файлами?](#72-как-filechannel-ускоряет-работу-с-файлами)
  - [7.3. Что такое zero-copy в NIO и как его использовать?](#73-что-такое-zero-copy-в-nio-и-как-его-использовать)
  - [7.4. Чем MappedByteBuffer отличается от обычного ByteBuffer?](#74-чем-mappedbytebuffer-отличается-от-обычного-bytebuffer)
  - [7.5. Что такое FileLock и зачем он нужен?](#75-что-такое-filelock-и-зачем-он-нужен)
  - [7.6. Что такое ScatteringByteChannel и GatheringByteChannel?](#76-что-такое-scatteringbytechannel-и-gatheringbytechannel)
- [8. Сериализация](#8-сериализация)
  - [8.1. Как сериализовать объект в файл (ObjectOutputStream)?](#81-как-сериализовать-объект-в-файл-objectoutputstream)
  - [8.2. Что такое transient и зачем он нужен?](#82-что-такое-transient-и-зачем-он-нужен)
  - [8.3. Как Serializable влияет на версионирование (serialVersionUID)?](#83-как-serializable-влияет-на-версионирование-serialversionuid)
  - [8.4. Чем опасна десериализация?](#84-чем-опасна-десериализация)
  - [8.5. Как использовать Externalizable вместо Serializable?](#85-как-использовать-externalizable-вместо-serializable)
  - [8.6. Как Sealed Classes и Records влияют на сериализацию?](#86-как-sealed-classes-и-records-влияют-на-сериализацию)
  - [8.7. Что такое readResolve() и writeReplace()? Как защитить синглтоны?](#87-что-такое-readresolve-и-writereplace-как-защитить-синглтоны)
  - [8.8. Как работает ObjectInputFilter (Java 9+) для защиты десериализации?](#88-как-работает-objectinputfilter-java-9-для-защиты-десериализации)
- [9. Классический сетевой I/O (Socket, ServerSocket)](#9-классический-сетевой-io-socket-serversocket)
  - [9.1. Как работает Socket и ServerSocket в классическом I/O?](#91-как-работает-socket-и-serversocket-в-классическом-io)
  - [9.2. Почему классическая модель плохо масштабируется (проблема C10k)?](#92-почему-классическая-модель-плохо-масштабируется-проблема-c10k)
- [10. NIO — основы (Channel, Buffer, Selector)](#10-nio--основы-channel-buffer-selector)
  - [10.1. Что такое NIO и чем он отличается от классического I/O?](#101-что-такое-nio-и-чем-он-отличается-от-классического-io)
  - [10.2. Какие три основных компонента есть в NIO?](#102-какие-три-основных-компонента-есть-в-nio)
  - [10.3. Как ByteBuffer работает в NIO?](#103-как-bytebuffer-работает-в-nio)
  - [10.4. Как переключить ByteBuffer между режимами записи и чтения?](#104-как-переключить-bytebuffer-между-режимами-записи-и-чтения)
  - [10.5. Что такое Direct Buffer и чем он отличается от Heap Buffer?](#105-что-такое-direct-buffer-и-чем-он-отличается-от-heap-buffer)
  - [10.6. Какие виды Channel существуют?](#106-какие-виды-channel-существуют)
  - [10.7. Какой Channel не поддерживает неблокирующий режим?](#107-какой-channel-не-поддерживает-неблокирующий-режим)
  - [10.8. Что такое неблокирующий режим в NIO?](#108-что-такое-неблокирующий-режим-в-nio)
  - [10.9. Как SocketChannel используется в неблокирующем режиме?](#109-как-socketchannel-используется-в-неблокирующем-режиме)
  - [10.10. Как работают slice(), duplicate() и asReadOnlyBuffer() у ByteBuffer?](#1010-как-работают-slice-duplicate-и-asreadonlybuffer-у-bytebuffer)
  - [10.11. Что такое ByteOrder (Big-Endian vs Little-Endian) в ByteBuffer?](#1011-что-такое-byteorder-big-endian-vs-little-endian-в-bytebuffer)
- [11. Мультиплексирование и Selector (Reactor Pattern)](#11-мультиплексирование-и-selector-reactor-pattern)
  - [11.1. Как работает Selector в NIO?](#111-как-работает-selector-в-nio)
  - [11.2. Как Selector помогает в мультиплексировании соединений?](#112-как-selector-помогает-в-мультиплексировании-соединений)
  - [11.3. Как реализовать простой NIO-сервер с ServerSocketChannel и Selector?](#113-как-реализовать-простой-nio-сервер-с-serversocketchannel-и-selector)
  - [11.4. Что такое SelectionKey и какие операции можно регистрировать?](#114-что-такое-selectionkey-и-какие-операции-можно-регистрировать)
- [12. Платформенно-зависимые механизмы мультиплексирования (epoll, kqueue, IOCP)](#12-платформенно-зависимые-механизмы-мультиплексирования-epoll-kqueue-iocp)
  - [12.1. Как Java использует epoll на Linux?](#121-как-java-использует-epoll-на-linux)
  - [12.2. Что такое kqueue и как Java использует его на macOS/BSD?](#122-что-такое-kqueue-и-как-java-использует-его-на-macosbsd)
  - [12.3. Как Java использует IOCP на Windows?](#123-как-java-использует-iocp-на-windows)
  - [12.4. Edge-triggered vs Level-triggered — что использует Java?](#124-edge-triggered-vs-level-triggered--что-использует-java)
  - [12.5. Как SelectorProvider выбирает реализацию?](#125-как-selectorprovider-выбирает-реализацию)
  - [12.6. Какие проблемы были с epoll в JDK и как их исправляли (epoll bug, JDK 21)?](#126-какие-проблемы-были-с-epoll-в-jdk-и-как-их-исправляли-epoll-bug-jdk-21)
  - [12.7. Что такое io_uring и будет ли он в Java?](#127-что-такое-io_uring-и-будет-ли-он-в-java)
- [13. NIO Pipe и DatagramChannel](#13-nio-pipe-и-datagramchannel)
  - [13.1. Что такое Pipe в NIO и для чего он нужен?](#131-что-такое-pipe-в-nio-и-для-чего-он-нужен)
  - [13.2. Что такое DatagramChannel?](#132-что-такое-datagramchannel)
- [14. Асинхронный I/O (AsynchronousChannel)](#14-асинхронный-io-asynchronouschannel)
  - [14.1. Что такое AsynchronousFileChannel и зачем он нужен?](#141-что-такое-asynchronousfilechannel-и-зачем-он-нужен)
  - [14.2. Как открыть файл в асинхронном режиме?](#142-как-открыть-файл-в-асинхронном-режиме)
  - [14.3. Какие операции поддерживает AsynchronousFileChannel?](#143-какие-операции-поддерживает-asynchronousfilechannel)
  - [14.4. Как обработать результат асинхронной операции (Future vs CompletionHandler)?](#144-как-обработать-результат-асинхронной-операции-future-vs-completionhandler)
  - [14.5. Какой пул потоков используется по умолчанию для асинхронных операций? Можно ли указать свой?](#145-какой-пул-потоков-используется-по-умолчанию-для-асинхронных-операций-можно-ли-указать-свой)
  - [14.6. Что такое AsynchronousSocketChannel и как реализовать асинхронный I/O?](#146-что-такое-asynchronoussocketchannel-и-как-реализовать-асинхронный-io)
  - [14.7. Как дождаться завершения всех асинхронных операций?](#147-как-дождаться-завершения-всех-асинхронных-операций)
  - [14.8. Какие исключения могут возникнуть при асинхронных операциях?](#148-какие-исключения-могут-возникнуть-при-асинхронных-операциях)
  - [14.9. Как избежать утечек памяти при работе с AsynchronousFileChannel?](#149-как-избежать-утечек-памяти-при-работе-с-asynchronousfilechannel)
  - [14.10. В каких сценариях AsynchronousFileChannel эффективнее синхронного I/O?](#1410-в-каких-сценариях-asynchronousfilechannel-эффективнее-синхронного-io)
- [15. Работа с ZIP-архивами](#15-работа-с-zip-архивами)
  - [15.1. Что такое ZipInputStream и ZipOutputStream?](#151-что-такое-zipinputstream-и-zipoutputstream)
  - [15.2. Как прочитать содержимое ZIP-архива с помощью ZipInputStream?](#152-как-прочитать-содержимое-zip-архива-с-помощью-zipinputstream)
  - [15.3. Как получить список файлов в ZIP-архиве без распаковки?](#153-как-получить-список-файлов-в-zip-архиве-без-распаковки)
  - [15.4. Как распаковать ZIP-архив в указанную директорию?](#154-как-распаковать-zip-архив-в-указанную-директорию)
  - [15.5. Что такое ZipFile и чем он отличается от ZipInputStream?](#155-что-такое-zipfile-и-чем-он-отличается-от-zipinputstream)
  - [15.6. Как проверить, что файл является ZIP-архивом?](#156-как-проверить-что-файл-является-zip-архивом)
  - [15.7. Как обработать вложенные (nested) ZIP-архивы?](#157-как-обработать-вложенные-nested-zip-архивы)
  - [15.8. Как обрабатывать пароли и шифрование в ZIP?](#158-как-обрабатывать-пароли-и-шифрование-в-zip)
  - [15.9. Что такое Zip Slip и как от него защититься?](#159-что-такое-zip-slip-и-как-от-него-защититься)
  - [15.10. Как ZipInputStream обрабатывает большие файлы (>4 ГБ, ZIP64)?](#1510-как-zipinputstream-обрабатывает-большие-файлы-4-гб-zip64)
- [16. RandomAccessFile](#16-randomaccessfile)
  - [16.1. Что такое RandomAccessFile и чем он отличается от FileInputStream/FileOutputStream?](#161-что-такое-randomaccessfile-и-чем-он-отличается-от-fileinputstreamfileoutputstream)
  - [16.2. Какие режимы открытия файла поддерживает RandomAccessFile?](#162-какие-режимы-открытия-файла-поддерживает-randomaccessfile)
  - [16.3. Как перемещаться по файлу с помощью seek() и узнать текущую позицию?](#163-как-перемещаться-по-файлу-с-помощью-seek-и-узнать-текущую-позицию)
  - [16.4. Как читать/писать примитивные типы (readInt, writeDouble) и строки?](#164-как-читатьписать-примитивные-типы-readint-writedouble-и-строки)
  - [16.5. Как редактировать файл в середине, не перезаписывая его полностью?](#165-как-редактировать-файл-в-середине-не-перезаписывая-его-полностью)
  - [16.6. Как реализовать простую БД на основе RandomAccessFile?](#166-как-реализовать-простую-бд-на-основе-randomaccessfile)
  - [16.7. В чём разница между режимами "rws" и "rwd"?](#167-в-чём-разница-между-режимами-rws-и-rwd)
  - [16.8. Почему RandomAccessFile медленнее, чем FileChannel + ByteBuffer? Как ускорить?](#168-почему-randomaccessfile-медленнее-чем-filechannel--bytebuffer-как-ускорить)
  - [16.9. RandomAccessFile vs FileChannel — что когда использовать?](#169-randomaccessfile-vs-filechannel--что-когда-использовать)
- [17. Virtual Threads и I/O (JDK 21+)](#17-virtual-threads-и-io-jdk-21)
  - [17.1. Как Virtual Threads меняют модель I/O в Java?](#171-как-virtual-threads-меняют-модель-io-в-java)
  - [17.2. Что такое pinning виртуальных потоков и как JDK 24 решает эту проблему?](#172-что-такое-pinning-виртуальных-потоков-и-как-jdk-24-решает-эту-проблему)
  - [17.3. Нужен ли NIO/Selector при использовании Virtual Threads?](#173-нужен-ли-nioselector-при-использовании-virtual-threads)
  - [17.4. Как Structured Concurrency (JEP 480) связано с I/O?](#174-как-structured-concurrency-jep-480-связано-с-io)
- [18. Модели ввода-вывода — сравнительный анализ](#18-модели-ввода-вывода--сравнительный-анализ)
  - [18.1. Blocking I/O (блокирующий ввод-вывод)](#181-blocking-io-блокирующий-ввод-вывод)
  - [18.2. Non-blocking I/O (неблокирующий ввод-вывод)](#182-non-blocking-io-неблокирующий-ввод-вывод)
  - [18.3. I/O Multiplexing (мультиплексирование — select/poll/epoll)](#183-io-multiplexing-мультиплексирование--selectpollepoll)
  - [18.4. Asynchronous I/O (асинхронный ввод-вывод)](#184-asynchronous-io-асинхронный-ввод-вывод)
  - [18.5. Сравнительная таблица всех моделей](#185-сравнительная-таблица-всех-моделей)
  - [18.6. Какую модель когда выбирать?](#186-какую-модель-когда-выбирать)
  - [18.7. io_uring — будущее асинхронного I/O в Linux и перспективы в Java](#187-io_uring--будущее-асинхронного-io-в-linux-и-перспективы-в-java)
- [19. Безопасность ввода-вывода](#19-безопасность-ввода-вывода)
  - [19.1. Что такое TOCTOU (Time-of-check to time-of-use) и как защищаться?](#191-что-такое-toctou-time-of-check-to-time-of-use-и-как-защищаться)
  - [19.2. Как безопасно создавать временные файлы?](#192-как-безопасно-создавать-временные-файлы)
  - [19.3. Чем опасны символические ссылки и как с ними работать?](#193-чем-опасны-символические-ссылки-и-как-с-ними-работать)
  - [19.4. Как InterruptibleChannel связан с прерыванием потоков?](#194-как-interruptiblechannel-связан-с-прерыванием-потоков)
- [20. Производительность и выбор подхода: дерево решений](#20-производительность-и-выбор-подхода-дерево-решений)
  - [20.1. Сравнение производительности: IO vs NIO vs Async vs Virtual Threads](#201-сравнение-производительности-io-vs-nio-vs-async-vs-virtual-threads)
  - [20.2. Дерево решений: какой I/O-подход выбрать для вашего сценария?](#202-дерево-решений-какой-io-подход-выбрать-для-вашего-сценария)
- [21. Эволюция I/O в JDK (7 → 26)](#21-эволюция-io-в-jdk-7--26)
- [22. Практические задачи (код)](#22-практические-задачи-код)
  - [22.1. Чтение последних N строк большого лог-файла](#221-чтение-последних-n-строк-большого-лог-файла)
  - [22.2. Многопоточное чтение разных частей файла через RandomAccessFile](#222-многопоточное-чтение-разных-частей-файла-через-randomaccessfile)
  - [22.3. Асинхронный логгер на AsynchronousFileChannel](#223-асинхронный-логгер-на-asynchronousfilechannel)
  - [22.4. Поиск строки в большом файле через RandomAccessFile](#224-поиск-строки-в-большом-файле-через-randomaccessfile)
  - [22.5. Рекурсивное копирование директории с NIO.2](#225-рекурсивное-копирование-директории-с-nio2)
  - [22.6. Распаковка ZIP-архива с защитой от Zip Slip](#226-распаковка-zip-архива-с-защитой-от-zip-slip)
  - [22.7. NIO-сервер с обработкой миллионов соединений на Virtual Threads](#227-nio-сервер-с-обработкой-миллионов-соединений-на-virtual-threads)
  - [22.8. Копирование InputStream → OutputStream с прогресс-баром (Java 9+)](#228-копирование-inputstream--outputstream-с-прогресс-баром-java-9)
  - [22.9. Простой парсер CSV с PushbackInputStream](#229-простой-парсер-csv-с-pushbackinputstream)
  - [22.10. Мониторинг свободного места на диске с FileStore](#2210-мониторинг-свободного-места-на-диске-с-filestore)

---

## 1. Основы Java I/O (Streams, Readers/Writers)

### 1.1. Что такое потоки (Stream) в Java I/O?

Поток (Stream) — это абстракция для последовательной передачи данных. Он представляет собой непрерывную череду байтов, идущих от источника (Source) к получателю (Destination). Ключевая особенность потоков в `java.io` — они **однонаправленные**: либо только читают (InputStream), либо только пишут (OutputStream).

**Как это работает на уровне ОС:**
Файловый или сетевой дескриптор, открытый операционной системой, оборачивается Java-объектом. Каждый вызов `read()` или `write()` в Java транслируется в системный вызов (`read(2)` / `write(2)` в POSIX). Системный вызов — это переключение из User Space в Kernel Space, что относительно дорого (сотни наносекунд). Именно поэтому буферизация критична для производительности.

**Иерархия потоков в java.io:**

```
InputStream (абстрактный)
├── FileInputStream          — чтение из файла
├── ByteArrayInputStream     — чтение из byte[]
├── BufferedInputStream      — декоратор, добавляет буферизацию
├── DataInputStream          — декоратор, читает примитивы (int, double, …)
├── ObjectInputStream        — декоратор, десериализация объектов
├── PipedInputStream         — межпоточный обмен
└── FilterInputStream        — базовый декоратор

OutputStream (абстрактный)
├── FileOutputStream
├── ByteArrayOutputStream
├── BufferedOutputStream
├── DataOutputStream
├── ObjectOutputStream
├── PipedOutputStream
└── FilterOutputStream

Reader (абстрактный, символьный)
├── FileReader               — чтение текста из файла
├── BufferedReader            — декоратор, буферизация
├── InputStreamReader         — мост: InputStream → Reader (с кодировкой)
├── CharArrayReader
├── StringReader
└── PipedReader

Writer (абстрактный, символьный)
├── FileWriter
├── BufferedWriter
├── OutputStreamWriter        — мост: Writer → OutputStream
├── CharArrayWriter
├── StringWriter
├── PrintWriter
└── PipedWriter
```

### 1.2. Какие основные классы есть в java.io (InputStream, OutputStream, Reader, Writer)?

- **InputStream** — базовый абстрактный класс для чтения байтовых данных. Ключевой метод: `int read()` (возвращает 0..255 или -1 при EOF). Есть методы `read(byte[])`, `read(byte[], off, len)`, `skip()`, `available()`, `close()`.
- **OutputStream** — базовый абстрактный класс для записи байтов. Ключевой метод: `void write(int b)` (пишет младшие 8 бит). Методы `write(byte[])`, `write(byte[], off, len)`, `flush()`, `close()`.
- **Reader** — базовый класс для чтения **символьных** данных (16-битный `char`). Аналог InputStream для текста. Ключевой метод `int read()` возвращает 0..65535 или -1.
- **Writer** — базовый класс для записи символов. Аналог OutputStream для текста.

**Почему появились Reader/Writer:** Изначально в Java 1.0 были только InputStream/OutputStream (байтовые). Но Java использует Unicode (16-битные `char`), и для работы с текстом требовалась обработка кодировок (UTF-8, CP1251, …). Поэтому в Java 1.1 добавили Reader/Writer, которые автоматически конвертируют байты в символы через `Charset`. Классы `InputStreamReader` и `OutputStreamWriter` — это **мост** между миром байтов и миром символов.

### 1.3. В чем разница между байтовыми (InputStream/OutputStream) и символьными (Reader/Writer) потоками?

| Характеристика | Байтовые (InputStream/OutputStream) | Символьные (Reader/Writer) |
|---|---|---|
| Единица данных | 1 байт (8 бит, 0..255) | 1 символ (char, 16 бит, 0..65535) |
| Что читают/пишут | "Сырые" байты без интерпретации | Символы Unicode с учётом кодировки |
| Кодировка | Не знают о кодировках | Используют Charset (UTF-8, ASCII, …) |
| Использование | Бинарные данные, изображения, видео, сериализация | Текст: .txt, .json, .xml, .csv |
| Производительность | Быстрее на байт (нет конвертации) | Медленнее (конвертация байты ↔ символы) |
| Примеры классов | FileInputStream, BufferedInputStream | FileReader, BufferedReader |
| Мост | InputStreamReader (InputStream → Reader) | OutputStreamWriter (Writer → OutputStream) |

**Важный нюанс:** `FileReader` **всегда** использует платформенную кодировку по умолчанию (`Charset.defaultCharset()`), которую нельзя переопределить. Это серьёзный недостаток. Правильный способ читать текст в нужной кодировке:

```java
// ❌ FileReader — всегда платформенная кодировка
try (Reader r = new FileReader("file.txt")) { … }

// ✅ Правильно: указываем кодировку явно
try (Reader r = new BufferedReader(
        new InputStreamReader(new FileInputStream("file.txt"), StandardCharsets.UTF_8))) { … }
```

### 1.4. Какой поток использовать для чтения текстовых файлов? А для бинарных?

**Текстовые файлы (.txt, .json, .xml, .csv, .yaml):**
- `Files.readString()` (Java 11+) — для небольших файлов: прочитать весь файл в строку одной командой
- `Files.readAllLines()` — прочитать все строки в `List<String>`
- `Files.lines()` — ленивый Stream строк, хорош для больших текстовых файлов
- `BufferedReader` — построчное чтение, классический подход
- `Scanner` — когда нужно парсить токены (числа, слова)

```java
// Java 11+: проще некуда
String content = Files.readString(Path.of("config.json"), StandardCharsets.UTF_8);

// Большой файл — построчно через Stream (лениво, не грузит всё в память)
try (Stream<String> lines = Files.lines(Path.of("huge.log"), StandardCharsets.UTF_8)) {
    lines.filter(l -> l.contains("ERROR")).forEach(System.out::println);
}

// Классический BufferedReader
try (BufferedReader br = new BufferedReader(
        new InputStreamReader(new FileInputStream("file.txt"), StandardCharsets.UTF_8))) {
    String line;
    while ((line = br.readLine()) != null) {
        // обрабатываем
    }
}
```

**Бинарные файлы (.jpg, .mp4, .class, .dat, .zip):**
- `Files.readAllBytes()` — для небольших бинарных файлов
- `FileInputStream + BufferedInputStream` — классический подход
- `FileChannel` — для больших файлов, random access, memory-mapping
- `Files.newInputStream()` / `Files.newOutputStream()` — NIO.2 способ

```java
// Небольшой бинарный файл
byte[] data = Files.readAllBytes(Path.of("image.jpg"));

// Большой бинарный файл — читаем чанками
try (InputStream in = Files.newInputStream(Path.of("large.dat"));
     BufferedInputStream bis = new BufferedInputStream(in)) {
    byte[] buf = new byte[8192];
    int read;
    while ((read = bis.read(buf)) != -1) {
        // обрабатываем read байт из buf
    }
}
```

### 1.5. Как работает try-with-resources и почему это важно для I/O?

`try-with-resources` (Java 7+) — конструкция, гарантирующая автоматическое закрытие ресурсов, реализующих `AutoCloseable` (или `Closeable`). Для I/O это критически важно, потому что незакрытые файловые/сетевые дескрипторы — это утечка ресурсов ОС.

**Как было до Java 7 (ужасно):**

```java
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
    // работа с br
} catch (IOException e) {
    // обработка
} finally {
    if (br != null) {
        try {
            br.close();  // close() тоже может бросить IOException!
        } catch (IOException e) {
            // ещё одна обработка
        }
    }
}
```

**Как стало с Java 7+:**

```java
// Один ресурс
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
}

// Несколько ресурсов — закрываются в порядке, обратном объявлению
try (FileInputStream fis = new FileInputStream("in.dat");
     BufferedInputStream bis = new BufferedInputStream(fis);
     FileOutputStream fos = new FileOutputStream("out.dat")) {
    // работа с потоками
}
// bis.close() → fis.close() → fos.close() — автоматически, даже при исключении
```

**Как это работает изнутри:**
Компилятор преобразует try-with-resources в обычный try-catch-finally. В блоке finally вызывается `close()` для каждого ресурса. Если и основное тело, и `close()` бросают исключения, то основное исключение сохраняется, а исключения от `close()` добавляются к нему как **suppressed** (доступны через `Throwable.getSuppressed()`). Это исправляет главную проблему ручного закрытия — потерю оригинального исключения.

### 1.6. Что такое паттерн Декоратор в java.io? Как он реализован?

**Паттерн Декоратор** — это структурный паттерн проектирования, который позволяет динамически добавлять поведение объекту, оборачивая его в другой объект. В `java.io` этот паттерн — основа всей архитектуры потоков.

**Как это реализовано:**

Базовые классы `FilterInputStream` и `FilterOutputStream` (а также `FilterReader`/`FilterWriter`) являются декораторами. Они содержат поле `protected InputStream in` (или `OutputStream out`) и делегируют ему все вызовы, добавляя своё поведение:

```
InputStream (абстрактный)
└── FilterInputStream (базовый декоратор)
    ├── BufferedInputStream     — добавляет буферизацию
    ├── DataInputStream         — добавляет чтение примитивов
    ├── ObjectInputStream       — добавляет десериализацию
    ├── PushbackInputStream     — добавляет "возврат" байтов
    └── CheckedInputStream      — добавляет контрольную сумму
```

```java
// Классический пример композиции декораторов:
// FileInputStream       — читает байты с диска
// BufferedInputStream   — добавляет буферизацию (читает блоками)
// DataInputStream       — добавляет чтение int, double, UTF
DataInputStream dis = new DataInputStream(
    new BufferedInputStream(
        new FileInputStream("data.bin")
    )
);

// Каждый слой добавляет свою функциональность:
// 1. FileInputStream.read() — системный вызов read(2)
// 2. BufferedInputStream.read() — загружает блок в память, отдаёт из памяти
// 3. DataInputStream.readInt() — читает 4 байта и собирает в int
```

**Почему это круто:**
- **Композиция vs наследование:** Вместо 2^n классов (FileBufferedDataInputStream) — просто комбинируем декораторы
- **Гибкость:** Можно добавить буферизацию к любому InputStream: файловому, сетевому, из byte[]
- **Single Responsibility:** Каждый декоратор делает что-то одно

```java
// Упрощённая реализация FilterInputStream (из JDK):
public class FilterInputStream extends InputStream {
    protected volatile InputStream in;  // оборачиваемый поток

    protected FilterInputStream(InputStream in) {
        this.in = in;
    }

    public int read() throws IOException {
        return in.read();  // делегирование
    }

    public void close() throws IOException {
        in.close();  // закрытие каскадно
    }
}

// BufferedInputStream переопределяет read() для добавления буферизации:
public class BufferedInputStream extends FilterInputStream {
    protected byte[] buf;
    protected int count;  // сколько байт прочитано в buf
    protected int pos;    // текущая позиция в buf

    public synchronized int read() throws IOException {
        if (pos >= count) {     // буфер исчерпан
            fill();             // читаем из ОС в буфер
            if (pos >= count) return -1;  // EOF
        }
        return buf[pos++] & 0xff;  // отдаём из памяти — БЫСТРО
    }
}
```

### 1.7. Как работают mark() и reset()? Какие потоки их поддерживают?

`mark()` и `reset()` позволяют **вернуться к ранее отмеченной позиции** в потоке — это нужно для парсеров и токенизаторов, которым надо «подсмотреть» вперёд (lookahead).

```java
// Типичный сценарий: проверяем, начинается ли поток с "MAGIC"
InputStream in = new BufferedInputStream(new FileInputStream("file.bin"));

in.mark(4);         // запоминаем позицию, разрешаем прочитать до 4 байт вперёд
byte[] magic = new byte[4];
in.read(magic);

if (magic[0] == 0xCA && magic[1] == 0xFE) {
    // Это наш формат — продолжаем чтение
} else {
    in.reset();      // Возвращаемся к mark — другой формат, пробуем иначе
    handleOtherFormat(in);
}
```

**Какие потоки поддерживают mark/reset:**

| Поток | mark/reset | Примечание |
|---|---|---|
| `BufferedInputStream` | ✅ Да | `mark(readlimit)` — гарантирует mark только на `readlimit` байт |
| `BufferedReader` | ✅ Да | Аналогично, но для символов |
| `ByteArrayInputStream` | ✅ Да (всегда) | Mark — это просто индекс в массиве |
| `FileInputStream` | ❌ Нет | `markSupported()` → `false` |
| `ObjectInputStream` | ❌ Нет | Не поддерживает |

**Как `markSupported()` помогает:**

```java
InputStream in = ...;
if (in.markSupported()) {
    in.mark(256);
    // можно использовать reset()
} else {
    // нужно вручную буферизовать данные: завернуть в BufferedInputStream
    in = new BufferedInputStream(in);  // теперь markSupported() → true!
}
```

**Важный нюанс `readlimit`:**
- В `BufferedInputStream.mark(readlimit)` параметр `readlimit` — это **подсказка**, а не жёсткое ограничение
- Если вы `mark(10)`, а потом прочитали 100 байт, `reset()` **может сработать**, если буфер достаточно большой, но **не гарантированно**
- Javadoc говорит: «если прочитано больше readlimit, reset может не сработать»

### 1.8. Что дают методы InputStream.readAllBytes() и transferTo() (Java 9+)?

Java 9 добавила два метода, которые радикально упрощают распространённые задачи:

**`InputStream.readAllBytes()`** — читает весь поток в `byte[]` одной строкой:
```java
// До Java 9: 6+ строк кода
byte[] allBytes;
try (InputStream in = new FileInputStream("file.bin")) {
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    byte[] buf = new byte[8192];
    int read;
    while ((read = in.read(buf)) != -1) {
        baos.write(buf, 0, read);
    }
    allBytes = baos.toByteArray();
}

// Java 9+: одна строка
byte[] allBytes = new FileInputStream("file.bin").readAllBytes();
```

⚠️ **Осторожно:** метод загружает всё в память — не используйте для гигабайтных файлов.

**`InputStream.transferTo(OutputStream)`** — копирует поток-в-поток одной строкой:
```java
// До Java 9:
try (InputStream in = new FileInputStream("source.dat");
     OutputStream out = new FileOutputStream("dest.dat")) {
    byte[] buf = new byte[8192];
    int read;
    while ((read = in.read(buf)) != -1) {
        out.write(buf, 0, read);
    }
}

// Java 9+:
try (InputStream in = new FileInputStream("source.dat");
     OutputStream out = new FileOutputStream("dest.dat")) {
    in.transferTo(out);  // всё!
}
```

**Внутренняя реализация `transferTo()`** делает ровно то же самое — цикл с буфером 8192 и копированием. Но код становится чище, и в будущем JVM сможет оптимизировать этот вызов (потенциально через zero-copy).

### 1.9. Что такое интерфейсы Flushable и Closeable?

Эти два интерфейса из `java.io` — основа управления жизненным циклом I/O-ресурсов:

**`Closeable` (extends AutoCloseable):**
```java
public interface Closeable extends AutoCloseable {
    void close() throws IOException;
}
```
- Гарантирует освобождение ресурсов (дескрипторы файлов, сокеты, нативную память)
- Идиоматический способ: try-with-resources
- `Closeable.close()` бросает `IOException` (в отличие от `AutoCloseable.close()`, который бросает `Exception`)
- Цепочка закрытий: закрытие декоратора закрывает обёрнутый поток

**`Flushable`:**
```java
public interface Flushable {
    void flush() throws IOException;
}
```
- Гарантирует, что буферизованные данные записаны в нижележащий поток/устройство
- Не все потоки поддерживают flush (например, `ByteArrayOutputStream.flush()` — no-op)
- Для `BufferedOutputStream`/`BufferedWriter`: сбрасывает внутренний буфер в обёрнутый поток
- Для `OutputStreamWriter`: сначала кодирует буфер, потом сбрасывает

```java
// flush() критичен при общении по сети:
try (Socket socket = new Socket("server", 8080);
     PrintWriter out = new PrintWriter(socket.getOutputStream())) {

    out.println("GET / HTTP/1.1");
    // Без flush() данные могут застрять в буфере и не уйти по сети
    out.flush();  // гарантирует отправку

    // Читаем ответ...
}
```

**Связь flush() и close():**
- `close()` **всегда вызывает `flush()`** перед закрытием (для OutputStream/Writer)
- Это гарантирует, что данные не потеряются при закрытии

---

## 2. Кодировки, Charset и мосты байты↔символы

### 2.1. Что такое Charset и как Java работает с кодировками?

**Charset** (character set) — это именованное соответствие между:
1. **Набором символов** (character repertoire) — какие символы поддерживаются
2. **Кодировкой** (encoding) — как каждый символ представляется в виде байтов

Класс `java.nio.charset.Charset` — центральный класс для работы с кодировками в Java:

```java
// Способы получения Charset:
Charset utf8 = StandardCharsets.UTF_8;           // лучший способ (Java 7+)
Charset utf8b = Charset.forName("UTF-8");         // по строковому имени
Charset defaultCharset = Charset.defaultCharset(); // платформенная кодировка (осторожно!)
Charset available = Charset.availableCharsets()   // все доступные (Map)
                  .get("windows-1251");

// Кодирование: String → byte[]
String text = "Привет, мир!";
byte[] utf8Bytes = text.getBytes(StandardCharsets.UTF_8);       // 21 байт (кириллица по 2)
byte[] winBytes = text.getBytes(Charset.forName("windows-1251")); // 12 байт (кириллица по 1)

// Декодирование: byte[] → String
String decoded1 = new String(utf8Bytes, StandardCharsets.UTF_8);
String decoded2 = new String(winBytes, Charset.forName("windows-1251"));
```

**Важнейшие стандартные кодировки (`StandardCharsets`):**

| Константа | Описание | Размер символа | Особенности |
|---|---|---|---|
| `UTF_8` | Unicode Transformation Format — 8 bit | 1–4 байта | Стандарт для Web, JSON, современных приложений |
| `UTF_16` | Unicode — 16 bit | 2 или 4 байта | Используется внутри Java (`char` = UTF-16 code unit) |
| `ISO_8859_1` | Latin-1 | 1 байт | Западноевропейские языки |
| `US_ASCII` | 7-bit ASCII | 1 байт | Только английский |
| `UTF_16BE` | UTF-16 Big-Endian | 2/4 байта | Старший байт первый |
| `UTF_16LE` | UTF-16 Little-Endian | 2/4 байта | Младший байт первый |

**Почему UTF-8 — стандарт де-факто:**
- Обратная совместимость с ASCII (первые 127 символов — 1 байт)
- Компактный для латиницы и многих европейских языков
- Нет проблем с порядком байтов (в отличие от UTF-16)
- Самосинхронизирующийся (можно найти начало символа даже при потере байта)

### 2.2. Что такое CharsetEncoder и CharsetDecoder? Зачем они нужны?

`CharsetEncoder` и `CharsetDecoder` — низкоуровневые классы для посимвольного/побайтового кодирования и декодирования. В отличие от простого `String.getBytes()`, они дают **полный контроль** над процессом:

```java
Charset charset = StandardCharsets.UTF_8;
CharsetEncoder encoder = charset.newEncoder();
CharsetDecoder decoder = charset.newDecoder();

// Настройка обработки ошибок:
encoder.onMalformedInput(CodingErrorAction.REPORT);   // ошибка при невалидном символе
encoder.onUnmappableCharacter(CodingErrorAction.REPLACE); // заменять непредставимые символы
encoder.replaceWith("?".getBytes());  // символ замены

decoder.onMalformedInput(CodingErrorAction.IGNORE);   // пропускать битые байты
decoder.onUnmappableCharacter(CodingErrorAction.REPORT); // ошибка при невалидном символе
```

**CodingErrorAction:**
- `REPORT` — бросить `CharacterCodingException`
- `IGNORE` — пропустить проблемный байт/символ
- `REPLACE` — заменить на символ-заменитель (обычно `?` или `\uFFFD`)

**Практический пример: фильтрация невалидного UTF-8:**

```java
// Допустим, файл частично повреждён — читаем то, что можем
CharsetDecoder lenientDecoder = StandardCharsets.UTF_8.newDecoder();
lenientDecoder.onMalformedInput(CodingErrorAction.IGNORE);
lenientDecoder.onUnmappableCharacter(CodingErrorAction.IGNORE);

try (FileChannel channel = FileChannel.open(Path.of("corrupted.txt"), READ)) {
    ByteBuffer buf = ByteBuffer.allocateDirect(4096);
    CharBuffer charBuf = CharBuffer.allocate(4096);

    while (channel.read(buf) != -1) {
        buf.flip();
        CoderResult result = lenientDecoder.decode(buf, charBuf, false);
        // result содержит информацию: overflow (charBuf мал), underflow (buf кончился),
        //                           malformed (пропущено), unmappable (пропущено)
        charBuf.flip();
        System.out.print(charBuf.toString());
        charBuf.clear();
        buf.compact();
    }
}
```

**Когда использовать CharsetEncoder/Decoder вместо простых методов:**
- Потоковая обработка (не держим весь файл в памяти)
- Контроль над обработкой ошибок (игнорировать/заменять/бросать)
- Обработка частичных данных (сетевые буферы, которые могут обрываться в середине символа)
- Производительность: можно переиспользовать буферы и кодеры/декодеры

### 2.3. Как работает InputStreamReader / OutputStreamWriter — мост байты↔символы?

`InputStreamReader` и `OutputStreamWriter` — это **мост** между миром байтов (`InputStream`/`OutputStream`) и миром символов (`Reader`/`Writer`). Без них невозможно читать текст из бинарных источников (файлы, сеть) с правильной кодировкой.

```java
// Мост: байты → символы
try (Reader reader = new InputStreamReader(
        new FileInputStream("file.txt"),   // байтовый источник
        StandardCharsets.UTF_8)) {          // как интерпретировать байты
    int ch;
    while ((ch = reader.read()) != -1) {
        System.out.print((char) ch);       // читаем символы, не байты!
    }
}

// Мост: символы → байты
try (Writer writer = new OutputStreamWriter(
        new FileOutputStream("file.txt"),   // байтовый приёмник
        StandardCharsets.UTF_8)) {           // как кодировать символы
    writer.write("Привет, мир!");           // символы автоматически → байты
}
```

**Как это работает внутри:**

`InputStreamReader.read()`:
1. Читает байты из обёрнутого `InputStream`
2. Накапливает их во внутреннем `ByteBuffer`
3. Декодирует через `CharsetDecoder` в `CharBuffer`
4. Возвращает очередной символ

`OutputStreamWriter.write(char)`:
1. Принимает `char`
2. Кодирует через `CharsetEncoder` в байты
3. Накапливает в буфере
4. При `flush()` или заполнении буфера — пишет в обёрнутый `OutputStream`

```java
// Классическая ошибка: FileReader без указания кодировки
// FileReader ВСЕГДА использует Charset.defaultCharset()!
try (Reader r = new FileReader("config.xml")) { ... }  // ❌ Кодировка зависит от ОС!

// Правильно: явно указываем кодировку
try (Reader r = new InputStreamReader(
        new FileInputStream("config.xml"), StandardCharsets.UTF_8)) { ... }  // ✅
```

### 2.4. Что такое BOM (Byte Order Mark) и как его обрабатывать?

**BOM** (Byte Order Mark) — это специальная последовательность байтов в начале текстового файла, которая обозначает:
1. Что файл в Unicode (UTF-8/UTF-16/UTF-32)
2. Порядок байтов (Big-Endian или Little-Endian для UTF-16/UTF-32)

| Кодировка | BOM (байты) | BOM (символ) |
|---|---|---|
| UTF-8 | `EF BB BF` | `U+FEFF` (в UTF-8 представлении) |
| UTF-16 BE | `FE FF` | `U+FEFF` |
| UTF-16 LE | `FF FE` | `U+FEFF` |
| UTF-32 BE | `00 00 FE FF` | `U+FEFF` |
| UTF-32 LE | `FF FE 00 00` | `U+FEFF` |

**Проблема BOM в Java:** Стандартный `CharsetDecoder` для UTF-8 **не игнорирует BOM автоматически** (в отличие от многих редакторов). Если файл содержит BOM, он будет прочитан как символ `\uFEFF` в начале строки:

```java
// Файл содержит: EF BB FF 48 65 6C 6C 6F (= BOM + "Hello")
String text = Files.readString(Path.of("file.txt"), StandardCharsets.UTF_8);
// text = "\uFEFFHello" — BOM стал частью строки! ❌

// Решение 1: Удалить BOM вручную
if (!text.isEmpty() && text.charAt(0) == '\uFEFF') {
    text = text.substring(1);
}

// Решение 2: Использовать Apache Commons IO
// String text = org.apache.commons.io.input.BOMInputStream(...)

// Решение 3: UnicodeReader — прочитать с автоопределением BOM
public static String readWithBOM(Path path) throws IOException {
    try (InputStream in = Files.newInputStream(path)) {
        byte[] bom = new byte[3];
        int read = in.read(bom);
        String encoding = "UTF-8";
        int skipBytes = 0;

        if (read >= 3 && bom[0] == (byte)0xEF && bom[1] == (byte)0xBB && bom[2] == (byte)0xBF) {
            encoding = "UTF-8";
            skipBytes = 3;
        } else if (read >= 2 && bom[0] == (byte)0xFE && bom[1] == (byte)0xFF) {
            encoding = "UTF-16BE";
            skipBytes = 2;
        } else if (read >= 2 && bom[0] == (byte)0xFF && bom[1] == (byte)0xFE) {
            encoding = "UTF-16LE";
            skipBytes = 2;
        }

        // Переоткрываем с правильной кодировкой
        try (InputStream in2 = Files.newInputStream(path)) {
            in2.skipNBytes(skipBytes);
            return new String(in2.readAllBytes(), Charset.forName(encoding));
        }
    }
}
```

### 2.5. Как определить кодировку текстового файла?

**Короткий ответ:** Надёжного способа **нет**. Кодировка — это метаданные, которые не хранятся в самом файле. Можно только **угадать** с той или иной степенью уверенности.

**Стратегии определения:**

**1. Проверка BOM:** если присутствует — см. раздел 2.4

**2. Статистический анализ (библиотеки):**
```java
// ICU4J (International Components for Unicode)
// Зависимость: com.ibm.icu:icu4j
import com.ibm.icu.text.CharsetDetector;
import com.ibm.icu.text.CharsetMatch;

byte[] data = Files.readAllBytes(Path.of("unknown.txt"));
CharsetDetector detector = new CharsetDetector();
detector.setText(data);
CharsetMatch match = detector.detect();
System.out.println("Кодировка: " + match.getName()        // "UTF-8"
    + ", уверенность: " + match.getConfidence());           // 0-100

// Альтернативы: juniversalchardet (Mozilla), Apache Tika EncodingDetector
```

**3. Эвристики:**
```java
// Проверка на валидность UTF-8:
public static boolean isValidUTF8(byte[] bytes) {
    try {
        StandardCharsets.UTF_8.newDecoder().decode(ByteBuffer.wrap(bytes));
        return true;
    } catch (CharacterCodingException e) {
        return false;
    }
}

// Если валидный UTF-8 → скорее всего UTF-8
// Если нет → пробуем windows-1251, ISO-8859-1, KOI8-R
```

**4. MIME-типы и HTTP-заголовки:** Для веб-контента кодировка указывается в `Content-Type`:
```
Content-Type: text/html; charset=utf-8
```

### 2.6. Какие проблемы возникают с платформенной кодировкой по умолчанию?

`Charset.defaultCharset()` возвращает кодировку ОС:
- **Windows:** обычно `windows-1251` (русская), `windows-1252` (западная)
- **Linux/macOS:** обычно `UTF-8`

**Проблема 1: Код работает на машине разработчика, но падает в продакшене**

```java
// На Windows: windows-1251 — работает с русским текстом
// На Linux: UTF-8 — тот же код ломается или выдаёт кракозябры
String text = new String(bytes);  // использует defaultCharset! ❌
```

**Проблема 2: `FileReader` — худший класс в java.io**

```java
// FileReader НЕЛЬЗЯ настроить на другую кодировку — всегда defaultCharset!
FileReader fr = new FileReader("config.xml");  // ❌ Никогда не используйте!
// Заменить на:
Reader fr = new InputStreamReader(new FileInputStream("config.xml"), StandardCharsets.UTF_8);
```

**Проблема 3: Разное поведение на разных JVM**

```java
// Даже на одной ОС, но с разными настройками локали
// java -Dfile.encoding=UTF-8
// java -Dfile.encoding=Cp1251
// → поведение одного и того же кода разное!
```

**Решение:** Всегда указывайте кодировку явно:
```java
// ✅ Явно
String text = new String(bytes, StandardCharsets.UTF_8);
Files.readString(path, StandardCharsets.UTF_8);
new InputStreamReader(in, StandardCharsets.UTF_8);
```

**JDK 18+**: `file.encoding` по умолчанию `UTF-8` независимо от ОС (JEP 400). Но полагаться на это можно только если вы уверены, что JDK ≥ 18.

---

## 3. Работа с файлами (File, Path, Files, NIO.2)

### 2.1. Чем java.io.File отличается от java.nio.file.Path (Java 7+)?

| Характеристика | `java.io.File` | `java.nio.file.Path` (NIO.2) |
|---|---|---|
| Появился | Java 1.0 | Java 7 (NIO.2) |
| Платформа | Привязан к платформенной ФС | Абстракция над любой ФС (включая ZIP, in-memory) |
| Ошибки | `boolean` (false при ошибке — непонятно, почему) | Исключения с описанием причины |
| Символические ссылки | Ограниченная поддержка | Полная поддержка (`LinkOption.NOFOLLOW_LINKS`) |
| Методы | Только базовые операции | Богатый API через утилитный класс `Files` |
| Иммутабельность | Мутабельный | Иммутабельный |
| Работа с путём | Строковые операции | `path.resolve()`, `path.relativize()`, `path.getParent()` |

```java
// Старый способ (java.io.File)
File file = new File("data/subdir/file.txt");
if (file.exists()) { /* ... */ }
file.delete();  // возвращает false — непонятно, почему не удалилось

// Новый способ (NIO.2)
Path path = Path.of("data/subdir/file.txt");  // Java 11+
// или Paths.get("data/subdir/file.txt")
if (Files.exists(path)) { /* ... */ }
try {
    Files.delete(path);  // NoSuchFileException, AccessDeniedException, …
} catch (IOException e) {
    // конкретная причина ошибки
}
```

### 2.2. Как прочитать файл в строку (String) с помощью Files?

```java
// Java 8: прочитать все строки в List
List<String> lines = Files.readAllLines(Path.of("file.txt"), StandardCharsets.UTF_8);

// Java 8: объединить строки в одну (с разделителем)
String content = String.join("\n", Files.readAllLines(Path.of("file.txt")));

// Java 11+: проще некуда — одна строка кода
String content = Files.readString(Path.of("file.txt"), StandardCharsets.UTF_8);

// Java 11+: с кодировкой по умолчанию (осторожно на Windows!)
String content = Files.readString(Path.of("file.txt"));
```

**Что внутри `Files.readString()`?** Он открывает `BufferedReader` через `Files.newBufferedReader()`, читает всё через `StringBuilder`, вызывает `close()`. Просто и надёжно, но не подходит для гигабайтных файлов.

### 2.3. Как записать данные в файл с помощью Files?

```java
// Java 7: запись байтов
byte[] data = "Hello, World!".getBytes(StandardCharsets.UTF_8);
Files.write(Path.of("file.txt"), data, StandardOpenOption.CREATE);

// Java 7: запись списка строк
List<String> lines = List.of("Line 1", "Line 2", "Line 3");
Files.write(Path.of("file.txt"), lines, StandardCharsets.UTF_8,
        StandardOpenOption.CREATE,
        StandardOpenOption.APPEND);   // дописывать, а не перезаписывать

// Java 11+: запись одной строки
Files.writeString(Path.of("file.txt"), "Hello, World!", StandardCharsets.UTF_8);

// Без опций — если файл существует и опций нет, будет java.nio.file.FileAlreadyExistsException
```

### 2.4. Как скопировать / переместить файл стандартными средствами Java?

```java
Path source = Path.of("source.txt");
Path target = Path.of("dest.txt");

// Копирование
Files.copy(source, target, StandardCopyOption.REPLACE_EXISTING);
// REPLACE_EXISTING — перезаписать, если целевой файл уже есть
// COPY_ATTRIBUTES  — скопировать метаданные (время, права)

// Перемещение (переименование)
Files.move(source, target, StandardCopyOption.REPLACE_EXISTING);
// ATOMIC_MOVE — атомарное перемещение (если ФС поддерживает), 
//               иначе исключение

// Копирование InputStream → файл (полезно для скачивания)
try (InputStream in = url.openConnection().getInputStream()) {
    Files.copy(in, Path.of("downloaded.dat"), StandardCopyOption.REPLACE_EXISTING);
}
```

### 2.5. Как рекурсивно обойти все файлы в директории?

**Способ 1: Stream API (простой, но без обработки ошибок обхода)**

```java
// Files.walk() — рекурсивный обход всего дерева
try (Stream<Path> paths = Files.walk(Path.of("/start/dir"))) {
    paths.filter(Files::isRegularFile)
         .forEach(System.out::println);
}

// С ограничением глубины (maxDepth = 3)
try (Stream<Path> paths = Files.walk(Path.of("/start/dir"), 3)) {
    paths.filter(Files::isRegularFile)
         .filter(p -> p.toString().endsWith(".java"))
         .forEach(System.out::println);
}
```

**Способ 2: Files.walkFileTree() (полный контроль, обработка ошибок)**

```java
Files.walkFileTree(Path.of("/start/dir"), new SimpleFileVisitor<>() {
    @Override
    public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs) {
        System.out.println("Входим в: " + dir);
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs) {
        System.out.println("  Файл: " + file + " (" + attrs.size() + " байт)");
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult visitFileFailed(Path file, IOException exc) {
        System.err.println("Не удалось прочитать: " + file);
        return FileVisitResult.CONTINUE;  // или TERMINATE / SKIP_SUBTREE
    }
});
```

**Способ 3: Files.find() (с предикатом из коробки)**

```java
// Найти все .java файлы, изменённые за последние 24 часа
Instant yesterday = Instant.now().minus(Duration.ofDays(1));
BiPredicate<Path, BasicFileAttributes> recentlyModified =
    (path, attrs) -> attrs.lastModifiedTime().toInstant().isAfter(yesterday)
                  && path.toString().endsWith(".java");

try (Stream<Path> found = Files.find(Path.of("/project"), 10, recentlyModified)) {
    found.forEach(System.out::println);
}
```

### 2.6. Как получить список файлов только текущей директории (не рекурсивно)?

```java
// Files.list() — только текущая директория, НЕ рекурсивно
try (Stream<Path> entries = Files.list(Path.of("/some/dir"))) {
    entries.filter(Files::isRegularFile)
           .forEach(System.out::println);
}

// Files.newDirectoryStream() — итератор, не Stream
try (DirectoryStream<Path> ds = Files.newDirectoryStream(Path.of("/some/dir"), "*.java")) {
    for (Path p : ds) {
        System.out.println(p);
    }
}
```

### 2.7. Как проверить, существует ли файл?

```java
Path path = Path.of("path/to/file");

// Простая проверка существования
boolean exists = Files.exists(path);

// Проверка: существует И это обычный файл (не директория, не ссылка)
boolean isFile = Files.isRegularFile(path);

// Проверка: существует И это директория
boolean isDir = Files.isDirectory(path);

// Проверка без перехода по символическим ссылкам
boolean existsNoFollow = Files.exists(path, LinkOption.NOFOLLOW_LINKS);

// Проверка прав
boolean readable = Files.isReadable(path);
boolean writable = Files.isWritable(path);
boolean executable = Files.isExecutable(path);
```

### 2.8. Как создать временный файл?

```java
// Создать временный файл
Path tmpFile = Files.createTempFile("prefix", ".tmp");
// Создаст что-то вроде: /tmp/prefix123456789.tmp

// Создать во временной директории, указанной явно
Path tmpDir = Path.of("/custom/tmp/dir");
Files.createDirectories(tmpDir);  // создаст все недостающие родительские директории
Path tmpFile = Files.createTempFile(tmpDir, "mydata", ".dat");

// Создать временную директорию
Path tmpDir = Files.createTempDirectory("myapp");

// ВАЖНО: временные файлы не удаляются автоматически.
// Их нужно удалять вручную или через tmpFile.toFile().deleteOnExit()
tmpFile.toFile().deleteOnExit();  // НО это утечка памяти для многих файлов!
// Лучше явно удалить в finally:
try {
    // работа с tmpFile
} finally {
    Files.deleteIfExists(tmpFile);
}
```

### 2.9. Как рекурсивно скопировать/удалить папку с NIO.2?

Для рекурсивного копирования/удаления директорий `Files.copy()` и `Files.delete()` недостаточно — они работают только с отдельными файлами. Нужно обойти дерево через `walkFileTree()`.

```java
// Рекурсивное копирование директории
Path sourceDir = Path.of("/source");
Path targetDir = Path.of("/target");

Files.walkFileTree(sourceDir, new SimpleFileVisitor<>() {
    @Override
    public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs)
            throws IOException {
        Path relativePath = sourceDir.relativize(dir);
        Files.createDirectories(targetDir.resolve(relativePath));
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
            throws IOException {
        Path relativePath = sourceDir.relativize(file);
        Files.copy(file, targetDir.resolve(relativePath),
                StandardCopyOption.REPLACE_EXISTING);
        return FileVisitResult.CONTINUE;
    }
});

// Рекурсивное удаление директории
Files.walkFileTree(dirToDelete, new SimpleFileVisitor<>() {
    @Override
    public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
            throws IOException {
        Files.delete(file);   // удаляем файл
        return FileVisitResult.CONTINUE;
    }

    @Override
    public FileVisitResult postVisitDirectory(Path dir, IOException exc)
            throws IOException {
        Files.delete(dir);    // удаляем пустую директорию
        return FileVisitResult.CONTINUE;
    }
});
```

### 2.10. Как мониторить изменения в файловой системе (WatchService)?

`WatchService` позволяет отслеживать изменения в директории: создание, модификацию и удаление файлов. Это аналог `inotify` в Linux или `ReadDirectoryChangesW` в Windows.

```java
WatchService watchService = FileSystems.getDefault().newWatchService();
Path watchedDir = Path.of("/path/to/watch");

// Регистрируем события для отслеживания
watchedDir.register(watchService,
        StandardWatchEventKinds.ENTRY_CREATE,
        StandardWatchEventKinds.ENTRY_MODIFY,
        StandardWatchEventKinds.ENTRY_DELETE);

while (true) {
    WatchKey key = watchService.take();  // блокируемся до события
    for (WatchEvent<?> event : key.pollEvents()) {
        WatchEvent.Kind<?> kind = event.kind();
        Path filename = (Path) event.context();

        if (kind == StandardWatchEventKinds.OVERFLOW) {
            // Часть событий потеряна — нужно полное сканирование
            System.err.println("OVERFLOW: пропущены события!");
            continue;
        }
        System.out.println(kind + ": " + filename);
    }
    if (!key.reset()) {
        break;  // директория удалена
    }
}
```

**Ограничения WatchService:**
- Не рекурсивный — нужно регистрировать каждую поддиректорию отдельно
- Зависит от ОС: на macOS реализация медленнее, чем на Linux
- Не все ФС поддерживают (сетевые диски, некоторые виртуальные ФС)
- Есть задержка между реальным изменением и уведомлением
- События могут сливаться (несколько модификаций → одно событие)

### 2.11. Как защититься от Path Traversal атак при работе с файлами?

Path Traversal (или Directory Traversal) — атака, при которой злоумышленник манипулирует путём файла, используя `../` для выхода за пределы разрешённой директории.

```java
// Базовая директория, куда разрешено писать
Path baseDir = Path.of("/safe/uploads").toRealPath();

// Пользовательский ввод
String userInput = "../../etc/passwd";  // атака!

// ❌ ОПАСНО: прямое использование пользовательского ввода
Path dangerous = baseDir.resolve(userInput);
// dangerous = /safe/uploads/../../etc/passwd → /etc/passwd

// ✅ БЕЗОПАСНО: проверка после нормализации
Path safe = baseDir.resolve(userInput).normalize();
if (!safe.startsWith(baseDir)) {
    throw new SecurityException("Path traversal detected: " + userInput);
}
// safe.normalize() = /etc/passwd → не начинается с /safe/uploads → исключение!

// Дополнительно: проверка на символические ссылки
Path real = safe.toRealPath();  // разрешает все символические ссылки
if (!real.startsWith(baseDir)) {
    throw new SecurityException("Symlink traversal detected!");
}
```

**Правила безопасной работы:**
1. Всегда нормализуй путь через `.normalize()`
2. Проверяй, что итоговый путь начинается с разрешённой базовой директории
3. Используй `.toRealPath()` для разрешения символических ссылок
4. Никогда не конкатенируй пользовательский ввод в пути напрямую (используй `resolve()`)

### 2.12. Какие StandardOpenOption бывают и зачем они нужны?

`StandardOpenOption` — enum, определяющий поведение при открытии файла через `Files.newInputStream()`, `Files.newOutputStream()`, `Files.write()`, `AsynchronousFileChannel.open()` и т.д.

| Опция | Описание |
|---|---|
| `READ` | Открыть для чтения |
| `WRITE` | Открыть для записи |
| `APPEND` | Дописывать в конец файла (указатель в конец) |
| `TRUNCATE_EXISTING` | Обрезать существующий файл до размера 0 |
| `CREATE` | Создать файл, если не существует |
| `CREATE_NEW` | Создать файл; если существует — выбросить `FileAlreadyExistsException` |
| `DELETE_ON_CLOSE` | Удалить файл при закрытии потока/канала |
| `SPARSE` | Подсказка ОС: файл будет разрежённым (sparse) |
| `SYNC` | Каждая запись синхронно на диск (данные + метаданные) |
| `DSYNC` | Каждая запись синхронно на диск (только данные) |

```java
// Типичные комбинации:
// Чтение
Files.newInputStream(path);  // READ
// Запись с созданием и перезаписью
Files.newOutputStream(path);  // WRITE, CREATE, TRUNCATE_EXISTING
// Дозапись в конец
Files.newOutputStream(path, StandardOpenOption.APPEND, StandardOpenOption.CREATE);
// Синхронная запись (аналог "rws" у RandomAccessFile)
FileChannel.open(path, WRITE, CREATE, SYNC);
```

### 2.13. Как Files.readString() и Files.writeString() упрощают работу с текстом (Java 11+)?

До Java 11 чтение/запись текстового файла требовало 3–5 строк шаблонного кода (открыть поток, обернуть в буфер, прочитать, закрыть). `Files.readString()` и `Files.writeString()` делают это в одну строку.

```java
// До Java 11: много шаблонного кода
String content;
try (BufferedReader br = Files.newBufferedReader(Path.of("file.txt"))) {
    StringBuilder sb = new StringBuilder();
    String line;
    while ((line = br.readLine()) != null) {
        sb.append(line).append("\n");
    }
    content = sb.toString();
}

// Java 11+: одна строка
String content = Files.readString(Path.of("file.txt"));

// Аналогично для записи:
Files.writeString(Path.of("file.txt"), "Hello", StandardCharsets.UTF_8,
        StandardOpenOption.APPEND);
```

**Ограничение:** оба метода загружают весь файл в память. Для файлов >100 МБ используйте `Files.lines()`, `Files.newBufferedReader()` или `FileChannel`.

### 2.14. Какой метод выбросит IOException при работе с Files.readAllLines()?

Сам `Files.readAllLines()` выбрасывает `IOException` в следующих случаях:
- `NoSuchFileException` (подкласс `IOException`) — файл не существует
- `AccessDeniedException` (подкласс `IOException`) — нет прав доступа
- Общая `IOException` — ошибка чтения диска, повреждённые данные и т.д.

Кроме того, если использовать `Files.lines()` (Stream API) и внутри лямбды произойдёт ошибка ввода-вывода, она будет обёрнута в `UncheckedIOException`, так как Stream API не пробрасывает checked-исключения напрямую:

```java
try (Stream<String> lines = Files.lines(path)) {
    lines.forEach(line -> {
        // IOException здесь обернётся в UncheckedIOException
    });
} catch (UncheckedIOException e) {
    IOException realCause = e.getCause();
}
```

### 2.15. Что произойдёт, если вызвать Files.delete() для несуществующего файла?

Будет выброшено `java.nio.file.NoSuchFileException` (подкласс `IOException`). Чтобы избежать этого, используйте `Files.deleteIfExists(path)`, который возвращает `true`, если файл существовал и был удалён, или `false`, если файла не было.

```java
// Бросит NoSuchFileException, если файла нет
Files.delete(Path.of("nonexistent.txt"));

// Безопасно: не бросает исключение, если файла нет
boolean deleted = Files.deleteIfExists(Path.of("maybe_exists.txt"));
```

### 2.16. Как работает Files.mismatch() (Java 12+) и зачем он нужен?

`Files.mismatch(Path, Path)` сравнивает два файла побайтово и возвращает:
- **-1L** — файлы идентичны
- **Первую позицию, где байты различаются** (начиная с 0)
- Работает быстро: использует `FileChannel` и сравнивает большими блоками в памяти

```java
long diffPos = Files.mismatch(Path.of("file1.bin"), Path.of("file2.bin"));
if (diffPos == -1) {
    System.out.println("Файлы идентичны");
} else {
    System.out.println("Файлы различаются в позиции: " + diffPos);
}
```

Это гораздо эффективнее, чем читать оба файла в память и сравнивать вручную.

---

## 4. Атрибуты файлов и метаданные файловой системы

### 4.1. Как читать атрибуты файла: BasicFileAttributes, DosFileAttributes, PosixFileAttributes?

NIO.2 предоставляет унифицированный способ чтения метаданных файла через `Files.readAttributes()`. Базовые атрибуты доступны на всех платформах; расширенные зависят от ОС.

**BasicFileAttributes** — доступны везде (Windows, Linux, macOS):

```java
Path path = Path.of("document.txt");
BasicFileAttributes attrs = Files.readAttributes(path, BasicFileAttributes.class);

System.out.println("Размер: " + attrs.size() + " байт");
System.out.println("Создан: " + attrs.creationTime());
System.out.println("Изменён: " + attrs.lastModifiedTime());
System.out.println("Доступ: " + attrs.lastAccessTime());
System.out.println("Файл? " + attrs.isRegularFile());
System.out.println("Директория? " + attrs.isDirectory());
System.out.println("Символическая ссылка? " + attrs.isSymbolicLink());
System.out.println("Другое? " + attrs.isOther());

// fileKey — уникальный идентификатор файла в ФС (inode на Linux)
System.out.println("FileKey: " + attrs.fileKey());
```

**DosFileAttributes** — специфичные для Windows (и некоторых Unix-ФС с эмуляцией DOS):

```java
try {
    DosFileAttributes dosAttrs = Files.readAttributes(path, DosFileAttributes.class);
    System.out.println("Read-only: " + dosAttrs.isReadOnly());
    System.out.println("Hidden: " + dosAttrs.isHidden());
    System.out.println("System: " + dosAttrs.isSystem());
    System.out.println("Archive: " + dosAttrs.isArchive());
} catch (UnsupportedOperationException e) {
    // Не Windows → эти атрибуты недоступны
}
```

**PosixFileAttributes** — для Linux/macOS/Unix:

```java
try {
    PosixFileAttributes posixAttrs = Files.readAttributes(path, PosixFileAttributes.class);
    System.out.println("Владелец: " + posixAttrs.owner());
    System.out.println("Группа: " + posixAttrs.group());
    System.out.println("Права: " + PosixFilePermissions.toString(posixAttrs.permissions()));
    // Права: "rwxr-xr--"
} catch (UnsupportedOperationException e) {
    // Не Unix → POSIX-атрибуты недоступны
}
```

**Как быстро прочитать базовые атрибуты без создания объекта:**

```java
// Отдельные атрибуты через статические методы Files:
long size = Files.size(path);                              // размер
FileTime lastModified = Files.getLastModifiedTime(path);   // время изменения
UserPrincipal owner = Files.getOwner(path);                // владелец
boolean isDir = Files.isDirectory(path);                   // директория?
boolean isHidden = Files.isHidden(path);                   // скрытый?
String probe = Files.probeContentType(path);               // MIME-тип (text/plain)
```

### 4.2. Как прочитать отдельные атрибуты через Files.readAttributes()?

Можно читать не весь набор, а **конкретные атрибуты по имени** — быстрее, если нужны не все:

```java
Path path = Path.of("file.txt");

// Читаем конкретные атрибуты по имени
Map<String, Object> attrs = Files.readAttributes(path, "size,lastModifiedTime,isDirectory");
// или: Files.readAttributes(path, "basic:size,lastModifiedTime"); — с префиксом "basic:"
// или: Files.readAttributes(path, "dos:hidden,readonly");         — Windows-атрибуты
// или: Files.readAttributes(path, "posix:permissions,owner");     — POSIX-атрибуты

System.out.println("size: " + attrs.get("size"));
System.out.println("lastModifiedTime: " + attrs.get("lastModifiedTime"));
System.out.println("isDirectory: " + attrs.get("isDirectory"));

// Установка атрибутов:
Files.setAttribute(path, "dos:readonly", true);   // сделать файл read-only
Files.setAttribute(path, "dos:hidden", false);     // снять скрытость
Files.setAttribute(path, "basic:lastModifiedTime",
    FileTime.fromMillis(System.currentTimeMillis()));  // обновить время изменения

// POSIX-права:
Files.setAttribute(path, "posix:permissions",
    PosixFilePermissions.fromString("rw-r--r--"));
```

**Имена атрибутов по категориям:**
- `basic:` — size, creationTime, lastModifiedTime, lastAccessTime, isDirectory, isRegularFile, isSymbolicLink, fileKey
- `dos:` — readonly, hidden, system, archive
- `posix:` — permissions, owner, group
- `owner:` — owner

### 4.3. Как получить информацию о файловой системе через FileStore?

`FileStore` представляет раздел/том файловой системы. Позволяет узнать общее и свободное место, тип ФС:

```java
// Получаем FileStore для конкретного пути
Path path = Path.of("/data/uploads");
FileStore store = Files.getFileStore(path);

System.out.println("Устройство: " + store.name());
System.out.println("Тип ФС: " + store.type());  // "NTFS", "ext4", "apfs", "zfs"
System.out.println("Всего места: " + store.getTotalSpace() / (1024*1024*1024) + " ГБ");
System.out.println("Свободно: " + store.getUsableSpace() / (1024*1024*1024) + " ГБ");
System.out.println("Не распределено: " + store.getUnallocatedSpace() / (1024*1024*1024) + " ГБ");
System.out.println("Только чтение: " + store.isReadOnly());

// Пройти по всем файловым хранилищам
for (FileStore fs : FileSystems.getDefault().getFileStores()) {
    System.out.printf("%s (%s): свободно %d ГБ из %d ГБ%n",
        fs.name(), fs.type(),
        fs.getUsableSpace() / (1024*1024*1024),
        fs.getTotalSpace() / (1024*1024*1024));
}
```

**Проверка перед записью — защита от переполнения диска:**

```java
public static void safeWrite(Path path, byte[] data) throws IOException {
    long requiredSpace = data.length + 10 * 1024 * 1024;  // +10 МБ запас
    long usable = Files.getFileStore(path).getUsableSpace();
    if (usable < requiredSpace) {
        throw new IOException("Недостаточно места на диске: требуется " +
            requiredSpace / (1024*1024) + " МБ, доступно " + usable / (1024*1024) + " МБ");
    }
    Files.write(path, data);
}
```

### 4.4. Как работать с владельцами файлов и правами доступа?

**Владельцы (UserPrincipal):**

```java
Path path = Path.of("secret.txt");

// Читаем владельца
UserPrincipal owner = Files.getOwner(path);
System.out.println("Владелец: " + owner.getName());

// Меняем владельца
UserPrincipal newOwner = FileSystems.getDefault()
    .getUserPrincipalLookupService()
    .lookupPrincipalByName("john");
Files.setOwner(path, newOwner);
```

**POSIX-права доступа:**

```java
// Читаем права
Set<PosixFilePermission> perms = Files.getPosixFilePermissions(path);
System.out.println("Права: " + PosixFilePermissions.toString(perms));  // rw-r--r--

// Проверяем конкретные права
boolean ownerRead = perms.contains(PosixFilePermission.OWNER_READ);
boolean ownerWrite = perms.contains(PosixFilePermission.OWNER_WRITE);
boolean otherRead = perms.contains(PosixFilePermission.OTHERS_READ);

// Устанавливаем права (как chmod 644 в Linux)
Set<PosixFilePermission> newPerms = PosixFilePermissions.fromString("rw-r--r--");
Files.setPosixFilePermissions(path, newPerms);

// Создаём файл сразу с нужными правами
Files.createFile(path, PosixFilePermissions.asFileAttribute(
    PosixFilePermissions.fromString("rw-------")));  // 600 — только владелец
```

### 4.5. Что такое PathMatcher и как фильтровать файлы по glob/regex?

`PathMatcher` — функциональный интерфейс для проверки пути на соответствие шаблону (`glob` или `regex`):

```java
FileSystem fs = FileSystems.getDefault();

// Glob-синтаксис (как в shell):
// *     — любые символы в пределах одного сегмента пути (кроме /)
// **    — любое количество сегментов пути (включая 0)
// ?     — один любой символ
// [abc] — один символ из набора
// {a,b} — одна из опций

// Создаём матчеры
PathMatcher javaFiles = fs.getPathMatcher("glob:**/*.java");       // все .java файлы
PathMatcher testFiles = fs.getPathMatcher("glob:**/*Test*.java");  // *Test*.java
PathMatcher deepFiles = fs.getPathMatcher("glob:/src/**/main/**"); // конкретная структура
PathMatcher regexMatcher = fs.getPathMatcher("regex:.*\\.(xml|json)"); // regex-вариант

// Использование с Files.walk():
try (Stream<Path> paths = Files.walk(Path.of("/project"))) {
    paths.filter(javaFiles::matches)
         .forEach(System.out::println);
}

// Использование с Files.find():
BiPredicate<Path, BasicFileAttributes> predicate =
    (path, attrs) -> javaFiles.matches(path) && attrs.size() < 1024 * 1024;
try (Stream<Path> found = Files.find(Path.of("/project"), 10, predicate)) {
    found.forEach(System.out::println);
}
```

### 4.6. Как монтировать ZIP/JAR как файловую систему через FileSystems.newFileSystem()?

Java позволяет работать с ZIP-архивом как с **обычной файловой системой** — читать, писать, обходить директории, не думая о формате ZIP:

```java
Path zipPath = Path.of("archive.zip");

// Открываем ZIP как файловую систему
try (FileSystem zipFs = FileSystems.newFileSystem(zipPath)) {
    // Работаем как с обычной ФС:
    Path root = zipFs.getPath("/");

    // Рекурсивно обходим все файлы внутри ZIP
    try (Stream<Path> entries = Files.walk(root)) {
        entries.filter(Files::isRegularFile)
               .forEach(p -> {
                   System.out.println("Файл в архиве: " + p);
                   try {
                       // Читаем содержимое напрямую!
                       String content = Files.readString(p);
                       System.out.println("  " + content.lines().count() + " строк");
                   } catch (IOException e) {
                       e.printStackTrace();
                   }
               });
    }

    // Создаём новый файл внутри ZIP
    Path newFile = zipFs.getPath("/new-file.txt");
    Files.writeString(newFile, "Hello from inside ZIP!");

    // Копируем файл в архив
    Path externalFile = Path.of("external-doc.txt");
    Path insideZip = zipFs.getPath("/docs/external-doc.txt");
    Files.createDirectories(insideZip.getParent());
    Files.copy(externalFile, insideZip);
}

// После закрытия FileSystem все изменения записаны в ZIP
```

**Ограничения:**
- ZIP-файловая система **только для чтения** по умолчанию (для записи нужно явно указать)
- Удаление файлов из ZIP не поддерживается стандартными средствами (только пересоздание)
- Производительность ниже, чем у обычной ФС (данные сжимаются/разжимаются на лету)

---

## 5. Буферизация и производительность

### 3.1. Что такое буферизация (BufferedReader, BufferedInputStream)? Зачем она нужна?

Буферизация — это накопление данных в промежуточном массиве (буфере) в оперативной памяти перед реальным чтением или записью. Без буферизации каждый вызов `read()` заставлял бы программу обращаться к диску или сети (системный вызов), что **очень медленно**.

**Почему системные вызовы дорогие:**
Каждый `read()` или `write()` в Java транслируется в системный вызов ОС. Системный вызов требует переключения из User Space в Kernel Space, сохранения/восстановления контекста процессора, и не может быть оптимизирован JIT-компилятором. Один системный вызов стоит ~100–500 наносекунд. Если читать файл побайтово, то для 1 МБ данных потребуется 1 миллион системных вызовов = ~0.1–0.5 секунд только на переключение контекста, без учёта времени самого чтения с диска.

**Как буферизация решает проблему:**
Buffered-обёртка считывает сразу большой блок (например, 8 КБ) в память одним системным вызовом, а затем отдаёт данные программе из памяти, без дополнительных системных вызовов. Для 1 МБ файла: ~128 системных вызовов вместо 1 000 000 — ускорение в ~8000 раз.

```java
// ❌ Без буфера: 1 системный вызов на каждый байт
try (InputStream in = new FileInputStream("file.bin")) {
    int b;
    while ((b = in.read()) != -1) {  // каждый read() → системный вызов!
        processByte(b);
    }
}

// ✅ С буфером: 1 системный вызов на каждые 8192 байта
try (InputStream in = new BufferedInputStream(new FileInputStream("file.bin"))) {
    int b;
    while ((b = in.read()) != -1) {  // read() из памяти, не из ОС
        processByte(b);
    }
}
```

### 3.2. Почему BufferedReader эффективнее FileReader?

`FileReader` (без буфера) делает запрос к ОС для **каждого** считываемого символа. Учитывая, что даже в ASCII каждый символ кодируется 1 байтом, а в UTF-8 русские буквы — 2 байтами, для чтения 1 МБ русского текста потребуется сотни тысяч системных вызовов.

`BufferedReader` делает **один** запрос к ОС для заполнения внутреннего буфера (по умолчанию 8192 символа = 16 КБ), а затем быстро отдаёт символы из оперативной памяти.

```java
// Внутреннее устройство BufferedReader.read() (упрощённо):
public int read() throws IOException {
    if (pos >= count) {          // буфер исчерпан?
        fill();                  // да — перечитываем из ОС в буфер
        if (pos >= count) return -1;  // EOF
    }
    return buf[pos++] & 0xff;    // отдаём из буфера
}
```

**Дополнительное преимущество BufferedReader:** метод `readLine()` читает целую строку за раз, что ещё эффективнее для текстовой обработки.

### 3.3. Как работает BufferedInputStream и какой размер буфера оптимален?

`BufferedInputStream` оборачивает другой `InputStream` и использует внутренний массив байтов. Механика работы:

1. При вызове `read()` проверяется, есть ли данные во внутреннем массиве `buf`.
2. Если буфер пуст (позиция чтения ≥ количества байт в буфере), вызывается `fill()`.
3. `fill()` читает из обёрнутого потока **один раз** большой блок данных в буфер.
4. Все последующие `read()` отдают данные из буфера без обращения к ОС.

**Размер буфера по умолчанию: 8192 байта (8 КБ).**

Это значение выбрано не случайно: 8192 — это размер страницы памяти во многих ОС (2 × 4096), что делает операции с буфером эффективными на уровне работы с памятью. Для современных SSD-дисков можно увеличить до 64 КБ или даже 256 КБ, но прирост будет всё менее заметен.

```java
// Стандартный размер
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("file.bin"));

// С указанием размера (например, 64 КБ для больших файлов на SSD)
BufferedInputStream bis = new BufferedInputStream(
        new FileInputStream("file.bin"), 65536);
```

**Оптимальный размер буфера по сценариям:**

| Сценарий | Рекомендуемый размер | Почему |
|---|---|---|
| Чтение с HDD | 8–64 КБ | Механическая задержка поиска доминирует |
| Чтение с SSD / NVMe | 64–256 КБ | Высокая пропускная способность |
| Сетевые потоки | 4–16 КБ | Зависит от MTU, буферов сокета |
| Оперативная память | 1–8 КБ | Нет смысла в больших буферах |

### 3.4. Как прочитать большой файл (1 ГБ+) без OutOfMemoryError?

**Нельзя** использовать методы, загружающие весь файл в память: `Files.readAllBytes()`, `Files.readAllLines()`, `Files.readString()`. Вместо этого нужно читать **потоково** — чанками (блоками) или построчно, не удерживая весь файл в памяти.

```java
// Способ 1: BufferedReader построчно (для текстовых файлов)
try (BufferedReader br = Files.newBufferedReader(Path.of("huge.log"))) {
    String line;
    while ((line = br.readLine()) != null) {
        processLine(line);  // обработали и забыли
    }
}

// Способ 2: Files.lines() — ленивый Stream (для текстовых)
try (Stream<String> lines = Files.lines(Path.of("huge.csv"))) {
    lines.filter(l -> l.contains("ERROR"))
         .limit(100)
         .forEach(System.out::println);
}  // Stream ленивый — строки читаются по мере необходимости

// Способ 3: Чтение чанками (для бинарных файлов)
try (InputStream in = Files.newInputStream(Path.of("huge.bin"));
     BufferedInputStream bis = new BufferedInputStream(in)) {
    byte[] buffer = new byte[65536];  // 64 КБ чанк
    int bytesRead;
    while ((bytesRead = bis.read(buffer)) != -1) {
        processChunk(buffer, bytesRead);
    }
}

// Способ 4: Memory-mapped файл через FileChannel (для случайного доступа)
try (FileChannel channel = FileChannel.open(
        Path.of("huge.dat"), StandardOpenOption.READ)) {
    MappedByteBuffer buf = channel.map(
            FileChannel.MapMode.READ_ONLY, 0, channel.size());
    // ОС сама подгружает страницы по требованию — не весь файл в памяти
}
```

### 5.5. Математика буферизации: сколько системных вызовов экономится?

**Расчёт для типичных сценариев:**

Исходные данные:
- Системный вызов `read(2)`: ~200–500 нс (на современных CPU)
- Чтение с NVMe-диска: ~10–100 мкс на операцию
- Размер буфера по умолчанию: 8192 байта (8 КБ)

**Пример: чтение файла размером 1 МБ (1 048 576 байт)**

| Подход | Системных вызовов | Время (сист. вызовы) | Время (диск) | Общее |
|---|---|---|---|---|
| Побайтовое чтение (`read()`) | 1 048 576 | ~0.5 сек | ~10 сек | **~10.5 сек** |
| byte[1024] без обёртки | 1 024 | ~0.5 мс | ~0.1 сек | **~0.1 сек** |
| BufferedInputStream (8 КБ) | 128 | ~64 мкс | ~10 мс | **~10 мс** |
| FileChannel + DirectBuffer | 16–128 | ~32 мкс | ~10 мс | **~10 мс** |
| MappedByteBuffer | 0+page faults | ~0 | ~10 мс | **~10 мс** |

**Ключевой вывод:** Разница между 1 048 576 и 128 системных вызовов — это разница между **10 секундами** и **10 миллисекундами** (1000x ускорение).

**Формула экономии:**
```
Количество системных вызовов = размер_файла / размер_буфера
Экономия = количество системных вызовов БЕЗ буфера - количество системных вызовов С буфером
```

**Практический бенчмарк:**

```java
public class BufferBenchmark {
    public static void main(String[] args) throws Exception {
        Path file = Files.createTempFile("bench", ".dat");
        byte[] data = new byte[100 * 1024 * 1024];  // 100 МБ
        Files.write(file, data);

        // 1. Без буфера
        long t1 = System.nanoTime();
        try (InputStream in = Files.newInputStream(file)) {
            while (in.read() != -1) { }  // 100 МЛН системных вызовов!
        }
        long t2 = System.nanoTime();
        System.out.printf("Без буфера: %,d мс%n", (t2 - t1) / 1_000_000);

        // 2. BufferedInputStream (8 КБ)
        t1 = System.nanoTime();
        try (InputStream in = new BufferedInputStream(Files.newInputStream(file))) {
            while (in.read() != -1) { }  // ~12 800 системных вызовов
        }
        t2 = System.nanoTime();
        System.out.printf("С буфером 8K: %,d мс%n", (t2 - t1) / 1_000_000);

        // 3. Свой буфер byte[65536]
        t1 = System.nanoTime();
        try (InputStream in = Files.newInputStream(file)) {
            byte[] buf = new byte[65536];
            while (in.read(buf) != -1) { }  // ~1 600 системных вызовов
        }
        t2 = System.nanoTime();
        System.out.printf("Буфер 64K: %,d мс%n", (t2 - t1) / 1_000_000);

        Files.delete(file);
    }
}
```

**Типичные результаты (100 МБ, NVMe SSD):**
- Без буфера: 8 000–15 000 мс
- BufferedInputStream (8 КБ): 50–150 мс
- Буфер 64 КБ: 40–100 мс

**Закон убывающей отдачи:** Увеличение буфера с 8 КБ до 64 КБ даёт прирост ~20–30%, а с 64 КБ до 1 МБ — всего ~5%. После определённого размера узким местом становится сам диск, а не количество системных вызовов.

---

## 6. Байтовые массивы и специализированные потоки

### 4.1. Что такое ByteArrayInputStream и ByteArrayOutputStream?

Это потоки, работающие **не с диском/сетью**, а с байтовым массивом в памяти.

- **`ByteArrayInputStream`** — читает байты из `byte[]`. Источник данных — массив в памяти. Полезен для тестирования или когда данные уже загружены в память.
- **`ByteArrayOutputStream`** — пишет байты во внутренний `byte[]`, который автоматически расширяется. В конце можно получить результат через `toByteArray()` или `writeTo(OutputStream)`.

```java
// Запись в массив
ByteArrayOutputStream baos = new ByteArrayOutputStream();
baos.write("Hello".getBytes(StandardCharsets.UTF_8));
baos.write(0xFF);  // запись байта
byte[] result = baos.toByteArray();   // {72, 101, 108, 108, 111, -1}

// Чтение из массива
ByteArrayInputStream bais = new ByteArrayInputStream(result);
int b;
while ((b = bais.read()) != -1) {
    System.out.printf("%02X ", b);
}
// Вывод: 48 65 6C 6C 6F FF

// Полезно: перехват данных, записанных в OutputStream
ByteArrayOutputStream capture = new ByteArrayOutputStream();
someMethodThatWritesTo(new PrintStream(capture));
String captured = capture.toString(StandardCharsets.UTF_8);
```

**Важно:** в отличие от файловых/сетевых потоков, `ByteArrayInputStream`/`ByteArrayOutputStream` не требуют закрытия (их `close()` — no-op), так как они не удерживают ресурсы ОС.

### 4.2. Что такое DataInputStream и DataOutputStream?

Это декораторы, позволяющие читать/писать **примитивные типы Java** (`int`, `long`, `double`, `boolean`, `String` через `readUTF`/`writeUTF`) в бинарном формате, пригодном для межплатформенного обмена (Big-Endian).

```java
// Запись
try (DataOutputStream dos = new DataOutputStream(
        new BufferedOutputStream(new FileOutputStream("data.bin")))) {
    dos.writeInt(42);        // 4 байта, Big-Endian
    dos.writeDouble(3.14);   // 8 байт
    dos.writeUTF("Привет");  // модифицированный UTF-8: длина (2 байта) + байты
    dos.writeBoolean(true);  // 1 байт
}

// Чтение — важно читать в том же порядке!
try (DataInputStream dis = new DataInputStream(
        new BufferedInputStream(new FileInputStream("data.bin")))) {
    int    i = dis.readInt();     // 42
    double d = dis.readDouble();  // 3.14
    String s = dis.readUTF();     // "Привет"
    boolean b = dis.readBoolean(); // true
}
```

**Формат `readUTF`/`writeUTF`:** Используется модифицированный UTF-8:
- 2 байта — длина строки в байтах
- Затем байты UTF-8 (но `\u0000` кодируется как 2 байта, а не как 1)

**Ограничение:** `readUTF`/`writeUTF` поддерживают строки длиной до 65535 байт в UTF-8.

### 4.3. Что такое PrintWriter и PrintStream?

Потоки для **форматированного текстового вывода**. Не выбрасывают `IOException` из методов `print`/`println`/`printf` — вместо этого нужно проверять флаг ошибки через `checkError()`.

- **`PrintStream`** (байтовый) — `System.out` и `System.err` являются PrintStream. Работает на уровне байтов, но имеет методы для вывода строк и примитивов. Появился в Java 1.0.
- **`PrintWriter`** (символьный) — появился в Java 1.1, предпочтительнее для текстового вывода, так как поддерживает кодировки. Имеет опцию `autoFlush`.

```java
// PrintWriter — для текста
try (PrintWriter pw = new PrintWriter(
        Files.newBufferedWriter(Path.of("report.txt"), StandardCharsets.UTF_8))) {
    pw.println("Отчёт");
    pw.printf("Значение: %d (%.2f%%)%n", 42, 12.5);
    if (pw.checkError()) {
        System.err.println("Ошибка записи!");
    }
}

// PrintStream — для совместимости с System.out
PrintStream ps = new PrintStream(Files.newOutputStream(Path.of("out.txt")));
ps.println("Hello");
ps.printf("%04d%n", 7);  // "0007"
```

**Различия PrintWriter vs PrintStream:**

| Характеристика | PrintWriter | PrintStream |
|---|---|---|
| Тип данных | Символьный (char) | Байтовый |
| Кодировка | Поддерживает (через Writer) | Использует платформенную |
| AutoFlush | Да (опционально) | Да (опционально) |
| Исключения | Не выбрасывает, checkError() | Не выбрасывает, checkError() |
| Когда использовать | Текстовые файлы, Unicode | System.out/err, совместимость |

### 4.4. Что такое PipedInputStream / PipedOutputStream?

Потоки для **межпоточного обмена данными** (Producer-Consumer в рамках одной JVM). Один поток пишет в `PipedOutputStream`, другой — читает из связанного `PipedInputStream`. Это классический способ передачи данных между потоками без использования общих коллекций.

```java
PipedOutputStream out = new PipedOutputStream();
PipedInputStream in = new PipedInputStream(out);  // связываем

// Поток-писатель
new Thread(() -> {
    try {
        out.write("Hello from another thread!".getBytes());
        out.close();
    } catch (IOException e) { /* ... */ }
}).start();

// Поток-читатель (main)
byte[] buf = new byte[1024];
int read = in.read(buf);
System.out.println(new String(buf, 0, read));
```

**Ограничения:**
- Потоки должны быть в разных потоках (Threads) — иначе deadlock
- Буфер ограничен (по умолчанию 1024 байта)
- При закрытии одного конца второй получает "broken pipe"

**Альтернатива в NIO:** класс `Pipe` (см. раздел 11).

### 4.5. Как работать с System.in, System.out, System.err?

Это стандартные потоки, открытые JVM при старте:

- **`System.in`** — `InputStream`, стандартный ввод (клавиатура, перенаправление из файла)
- **`System.out`** — `PrintStream`, стандартный вывод
- **`System.err`** — `PrintStream`, стандартный вывод ошибок (не буферизован)

```java
// Чтение с консоли (построчно)
try (BufferedReader reader = new BufferedReader(
        new InputStreamReader(System.in, StandardCharsets.UTF_8))) {
    String line;
    System.out.print("Введите команду: ");
    while ((line = reader.readLine()) != null) {
        System.out.println("Вы ввели: " + line);
        if ("exit".equals(line)) break;
        System.out.print("Введите команду: ");
    }
}

// Scanner — удобнее для парсинга
try (Scanner scanner = new Scanner(System.in)) {
    System.out.print("Введите число: ");
    int n = scanner.nextInt();
    System.out.println("Квадрат: " + (n * n));
}
```

**Не закрывайте `System.in`/`System.out`/`System.err` вручную!** После закрытия их нельзя переоткрыть в рамках этого процесса.

### 6.6. Что такое PushbackInputStream / PushbackReader и зачем они нужны?

Это потоки, которые позволяют **«вернуть»** прочитанные байты/символы обратно в поток. Критически полезны для парсеров и токенизаторов, которым нужно «подсмотреть» вперёд (lookahead):

```java
// Парсер чисел: если после цифр идёт не цифра — "возвращаем" её обратно
PushbackInputStream pbis = new PushbackInputStream(
    new ByteArrayInputStream("42abc".getBytes()), 4);  // размер pushback-буфера

int b;
while ((b = pbis.read()) != -1) {
    if (b >= '0' && b <= '9') {
        int value = b - '0';
        // Смотрим следующий байт
        int next = pbis.read();
        if (next >= '0' && next <= '9') {
            value = value * 10 + (next - '0');
        } else if (next != -1) {
            pbis.unread(next);  // ВОЗВРАЩАЕМ — это не цифра, пригодится позже
        }
        System.out.println("Число: " + value);
    } else {
        System.out.println("Символ: " + (char) b);
    }
}
// Вывод: Число: 42, Символ: a, Символ: b, Символ: c
```

**Методы unread():**
```java
pbis.unread(byte);     // вернуть один байт
pbis.unread(byte[]);   // вернуть массив байтов
pbis.unread(byte[], off, len);  // вернуть часть массива

// PushbackReader — то же самое для символов:
PushbackReader pbr = new PushbackReader(new StringReader("Hello"), 4);
int c = pbr.read();     // 'H'
pbr.unread(c);          // вернули обратно
c = pbr.read();         // снова 'H'
```

**Когда использовать:**
- Парсинг чисел из смешанного потока (числа + текст)
- Реализация лексических анализаторов (tokenizers)
- Обработка протоколов, где нужно определить тип следующего сообщения по первому байту

### 6.7. Что такое SequenceInputStream и как объединить несколько потоков?

`SequenceInputStream` склеивает несколько `InputStream` в один — читает первый до EOF, затем автоматически переходит ко второму, и т.д.:

```java
// Объединение двух потоков
try (InputStream in1 = new FileInputStream("part1.txt");
     InputStream in2 = new FileInputStream("part2.txt");
     InputStream combined = new SequenceInputStream(in1, in2)) {

    byte[] all = combined.readAllBytes();
    System.out.println(new String(all));
}

// Объединение N потоков через Enumeration
List<InputStream> streams = List.of(
    new FileInputStream("chunk1.bin"),
    new FileInputStream("chunk2.bin"),
    new FileInputStream("chunk3.bin")
);
Enumeration<InputStream> enumeration = Collections.enumeration(streams);
try (InputStream megaStream = new SequenceInputStream(enumeration)) {
    // Читает все три файла как один непрерывный поток
    megaStream.transferTo(new FileOutputStream("combined.bin"));
}
```

**Применение:**
- Склеивание файлов, разбитых на чанки
- Объединение данных из нескольких источников
- Чтение логов из нескольких файлов как из одного

**С Java 9+ есть альтернатива без SequenceInputStream:**

```java
// Через Stream API и последовательное копирование:
try (OutputStream out = new FileOutputStream("combined.bin")) {
    for (Path p : List.of(Path.of("chunk1"), Path.of("chunk2"), Path.of("chunk3"))) {
        try (InputStream in = Files.newInputStream(p)) {
            in.transferTo(out);
        }
    }
}
```

### 6.8. Что такое StringReader / StringWriter и CharArrayReader / CharArrayWriter?

Это символьные аналоги `ByteArrayInputStream`/`ByteArrayOutputStream`:

| Байтовые | Символьные | Источник/Приёмник |
|---|---|---|
| `ByteArrayInputStream` | `StringReader` / `CharArrayReader` | Чтение из памяти |
| `ByteArrayOutputStream` | `StringWriter` / `CharArrayWriter` | Запись в память |

```java
// StringReader — читает символы из строки
StringReader sr = new StringReader("Hello\nWorld");
try (BufferedReader br = new BufferedReader(sr)) {
    br.lines().forEach(System.out::println);
}

// StringWriter — собирает вывод в строку
StringWriter sw = new StringWriter();
sw.write("Line 1\n");
sw.write("Line 2\n");
sw.append("Appended text");
String result = sw.toString();   // "Line 1\nLine 2\nAppended text"

// CharArrayReader / CharArrayWriter — то же, но с char[]
char[] data = {'H', 'e', 'l', 'l', 'o'};
CharArrayReader car = new CharArrayReader(data);

CharArrayWriter caw = new CharArrayWriter();
caw.write("Test");
char[] written = caw.toCharArray();
```

**Типичный сценарий — перехват вывода в String:**

```java
// Метод ожидает Writer, а нам нужен String
StringWriter capture = new StringWriter();
printReport(new PrintWriter(capture));  // метод пишет в Writer
String report = capture.toString();      // забираем результат
```

### 6.9. Как работает Console (System.console()) для защищённого ввода?

`System.console()` возвращает единственный экземпляр `java.io.Console` (или `null`, если JVM запущена без консоли).

```java
Console console = System.console();
if (console == null) {
    System.err.println("Консоль недоступна (запущено из IDE или перенаправлен ввод)");
    return;
}

// Форматированный вывод
console.printf("Добро пожаловать, %s!%n", System.getProperty("user.name"));

// Чтение строки
String login = console.readLine("Логин: ");
System.out.println("Введено: " + login);

// Защищённое чтение пароля — символы не отображаются на экране!
char[] password = console.readPassword("Пароль: ");
// Важно: пароль в char[], а не в String
// char[] можно затереть после использования, String — нет (интернирование)

// Проверка пароля
boolean ok = verifyPassword(login, password);

// СТИРАЕМ пароль из памяти сразу после проверки!
Arrays.fill(password, ' ');

// Форматированный вывод
console.format("Результат: %s%n", ok ? "OK" : "FAIL");
```

**Почему `char[]` для пароля, а не `String`:**
- `String` иммутабелен и может попасть в пул строк — останется в памяти надолго
- `char[]` можно затереть `Arrays.fill()` сразу после использования
- Дампы памяти не будут содержать пароль в открытом виде

**Когда `System.console()` возвращает `null`:**
- Приложение запущено из IDE (Eclipse, IntelliJ)
- Ввод/вывод перенаправлены (`java MyApp < input.txt`)
- JVM запущена без терминала

### 6.10. Что такое LineNumberReader и как отслеживать номера строк?

`LineNumberReader` — декоратор над `BufferedReader`, который автоматически отслеживает номер текущей строки:

```java
try (LineNumberReader lnr = new LineNumberReader(
        new InputStreamReader(new FileInputStream("script.sql"), StandardCharsets.UTF_8))) {

    lnr.setLineNumber(1);  // начинаем с 1-й строки

    String line;
    while ((line = lnr.readLine()) != null) {
        int lineNum = lnr.getLineNumber();

        if (line.trim().isEmpty()) {
            continue;  // номер строки увеличивается, но мы пропускаем
        }

        System.out.printf("%4d: %s%n", lineNum, line);

        // Синтаксическая ошибка — показываем точную строку!
        if (line.contains("DROOP TABLE")) {
            throw new SQLSyntaxErrorException(
                "Ошибка в строке " + lineNum + ": " + line);
        }

        // setLineNumber() для перепривязки (например, после включения другого файла)
        if (line.startsWith("--#include")) {
            lnr.setLineNumber(1);  // сброс счётчика для включаемого файла
        }
    }
}
```

**По умолчанию нумерация начинается с 0.** Всегда вызывайте `setLineNumber(1)` если хотите с 1.

**Альтернатива — Stream API (Java 8+)** не даёт номеров строк напрямую, но можно имитировать:

```java
// Эмуляция LineNumberReader через Stream API
AtomicInteger counter = new AtomicInteger(1);
try (Stream<String> lines = Files.lines(Path.of("script.sql"))) {
    lines.forEach(line -> {
        int num = counter.getAndIncrement();
        System.out.printf("%4d: %s%n", num, line);
    });
}
```

---

## 7. FileChannel и Memory Mapping

### 5.1. Что такое FileChannel? Какие возможности даёт?

`FileChannel` — это канал для работы с файлами в NIO. В отличие от `FileInputStream`/`FileOutputStream`, FileChannel:

- **Двунаправленный** (можно и читать, и писать через один объект)
- **Позиционируемый** — произвольный доступ через `position()`
- **Поддерживает Memory-Mapping** — отображение файла в память
- **Поддерживает Zero-Copy** — `transferTo()` / `transferFrom()`
- **Поддерживает блокировки файлов** — `lock()` / `tryLock()`
- **Работает с ByteBuffer** — данными напрямую, без потоковой абстракции

```java
// Открытие FileChannel
try (FileChannel channel = FileChannel.open(
        Path.of("data.bin"),
        StandardOpenOption.READ,
        StandardOpenOption.WRITE,
        StandardOpenOption.CREATE)) {

    // Чтение в ByteBuffer
    ByteBuffer buf = ByteBuffer.allocate(1024);
    int bytesRead = channel.read(buf);
    buf.flip();

    // Запись из ByteBuffer
    ByteBuffer writeBuf = ByteBuffer.wrap("Hello".getBytes());
    channel.write(writeBuf);

    // Произвольное позиционирование
    channel.position(100);    // переместиться на байт 100
    long pos = channel.position();  // узнать текущую позицию
    long size = channel.size();     // размер файла

    // Обрезать файл
    channel.truncate(1024);   // обрезать до 1024 байт

    // Принудительно сбросить на диск
    channel.force(true);      // true = включая метаданные
}
```

**Как получить FileChannel из старых потоков:**

```java
FileChannel ch1 = new FileInputStream("file").getChannel();
FileChannel ch2 = new FileOutputStream("file").getChannel();
FileChannel ch3 = new RandomAccessFile("file", "rw").getChannel();
```

### 5.2. Как FileChannel ускоряет работу с файлами?

FileChannel быстрее классических потоков по нескольким причинам:

1. **Прямая работа с буферами:** `ByteBuffer` (особенно Direct) минимизирует копирование данных между Java-кучей и нативными структурами ОС.

2. **Блочные операции:** `read(ByteBuffer)` и `write(ByteBuffer)` оперируют блоками данных, а не отдельными байтами. Меньше системных вызовов.

3. **Memory-Mapped файлы:** `map()` отображает файл напрямую в виртуальную память процесса. ОС подгружает страницы по требованию (demand paging). Данные читаются/пишутся напрямую в память, без явных системных вызовов.

4. **Zero-Copy:** `transferTo()` и `transferFrom()` копируют данные между каналами внутри ядра ОС, не загружая их в пространство пользователя.

5. **Позиционирование без Seek:** Позиция чтения/записи управляется через Java-объект, без системных вызовов `lseek`.

6. **Scatter/Gather:** `read(ByteBuffer[])` и `write(ByteBuffer[])` за один системный вызов читают/пишут в несколько буферов.

### 5.3. Что такое zero-copy в NIO и как его использовать?

**Zero-copy** — технология, позволяющая передавать данные (например, из файла в сокет) **без копирования в пространство пользователя** (User Space). Данные перемещаются напрямую внутри ядра ОС (Kernel Space).

**Традиционный путь копирования файл → сеть (4 копирования, 2 системных вызова):**
```
Диск → DMA → Kernel Buffer → [CPU copy] → User Buffer → [CPU copy] → Socket Buffer → DMA → Сеть
```

**Zero-copy через `transferTo()` (2 копирования DMA, 0 CPU-копирований):**
```
Диск → DMA → Kernel Buffer → [DMA copy] → Socket Buffer → DMA → Сеть
```

```java
// Отправка файла через HTTP без лишнего копирования
try (ServerSocketChannel server = ServerSocketChannel.open();
     FileChannel fileChannel = FileChannel.open(Path.of("large_video.mp4"))) {

    server.bind(new InetSocketAddress(8080));
    SocketChannel client = server.accept();

    long position = 0;
    long fileSize = fileChannel.size();

    // transferTo — zero-copy: данные из файла → сокет внутри ядра
    while (position < fileSize) {
        position += fileChannel.transferTo(position, fileSize - position, client);
    }
}

// Копирование файл → файл через transferFrom
try (FileChannel src = FileChannel.open(Path.of("source.dat"), READ);
     FileChannel dst = FileChannel.open(Path.of("dest.dat"), WRITE, CREATE)) {
    src.transferTo(0, src.size(), dst);
    // или: dst.transferFrom(src, 0, src.size());
}
```

**Ограничения `transferTo()`:**
- На Linux до JDK 8 мог передать только 2 ГБ за один вызов — нужно вызывать в цикле
- Некоторые ОС/ФС могут не поддерживать zero-copy для определённых типов файлов
- Требует `FileChannel` (не работает с произвольным `Channel`)

### 5.4. Чем MappedByteBuffer отличается от обычного ByteBuffer?

`MappedByteBuffer` — это особый вид буфера, который отображает участок файла прямо в виртуальную память процесса. Это не копия данных, а **прямое окно в файл** через механизм виртуальной памяти ОС.

**Как работает memory-mapping:**
1. Вызов `channel.map()` сообщает ОС: «отобрази этот диапазон файла в память»
2. ОС **не читает** файл сразу. Она выделяет диапазон виртуальных адресов и связывает их с файлом.
3. При первом обращении к памяти происходит **page fault** — ОС подгружает соответствующую страницу файла с диска.
4. Изменения в памяти **могут быть** (но не сразу) записаны обратно на диск. Принудительно — через `MappedByteBuffer.force()`.

```java
// Отображение файла в память
try (FileChannel channel = FileChannel.open(
        Path.of("large.dat"), StandardOpenOption.READ, StandardOpenOption.WRITE)) {

    // Отображаем 100 МБ, начиная с позиции 0
    MappedByteBuffer buf = channel.map(
            FileChannel.MapMode.READ_WRITE,  // READ_ONLY / READ_WRITE / PRIVATE
            0,                                 // начальная позиция в файле
            100 * 1024 * 1024);                // размер отображения

    // Читаем — данные подгружаются по требованию (page fault)
    byte firstByte = buf.get(0);

    // Пишем — изменения отражаются в файле (не мгновенно, через page cache)
    buf.put(100, (byte) 0xFF);

    // Принудительно сбросить изменения на диск
    buf.force();
}
```

**Отличия MappedByteBuffer от обычного HeapByteBuffer:**

| Характеристика | MappedByteBuffer | HeapByteBuffer |
|---|---|---|
| Где данные | Виртуальная память → файл на диске | Java Heap (byte[]) |
| Загрузка | По требованию (page fault) | Вся сразу при создании |
| Размер | До 2 ГБ одним маппингом (ограничение int) | Ограничен доступной кучей |
| GC | Не нагружает GC | Может вызывать GC при больших размерах |
| Освобождение | Сложно (см. ниже) | GC собирает автоматически |
| Изменения на диск | Через page cache + `force()` | Нужно явно писать |

**Важная проблема — освобождение MappedByteBuffer:**

MappedByteBuffer не освобождается сразу при вызове `close()` на FileChannel. Память виртуального адресного пространства удерживается до тех пор, пока GC не соберёт объект буфера **и** не вызовет `Cleaner`. Это может привести к исчерпанию виртуальной памяти при частых маппингах. Решения:

```java
// Освобождение MappedByteBuffer вручную (hack, но работает):
import sun.misc.Unsafe;
import java.lang.reflect.Field;

public static void unmap(MappedByteBuffer buffer) {
    // Через Cleaner (JDK 9+):
    // sun.misc.Unsafe.invokeCleaner(buffer);
    // Или через прямой доступ к Cleaner (JDK 8):
    // Метод cleaner() → clean()
}
```

Начиная с JDK 14, `FileChannel.map()` может создавать `MappedByteBuffer`, который можно освободить через встроенный `Cleaner` из пакета `jdk.internal.ref.Cleaner`, но публичного API для этого всё ещё нет.

### 5.5. Что такое FileLock и зачем он нужен?

`FileLock` представляет блокировку файла (или его части) на уровне операционной системы, предотвращая одновременную модификацию из разных процессов. Это не то же самое, что `synchronized` или `ReentrantLock` в Java — `FileLock` работает **между разными JVM/процессами**.

```java
try (FileChannel channel = FileChannel.open(
        Path.of("shared.db"), WRITE, CREATE);
     FileLock lock = channel.lock()) {  // эксклюзивная блокировка всего файла

    // Только этот процесс может писать в файл
    channel.write(ByteBuffer.wrap("safe write".getBytes()));

}  // lock.close() освободит блокировку автоматически

// Неблокирующая попытка захвата
try (FileChannel channel = FileChannel.open(Path.of("shared.db"), WRITE)) {
    FileLock lock = channel.tryLock();  // null если файл уже заблокирован
    if (lock != null) {
        try {
            // работаем
        } finally {
            lock.release();  // или lock.close()
        }
    }
}

// Блокировка части файла
FileLock lock = channel.lock(0, 1024, false);  // 0-1024 байты, shared lock
```

**Виды блокировок:**
- **Exclusive lock** (`lock()`) — только один процесс может писать; другие не могут читать или писать
- **Shared lock** (`lock(0, Long.MAX_VALUE, false)`) — несколько процессов могут читать; писатели блокируются

**Ограничения:**
- На некоторых ОС блокировки **advisory** (рекомендательные) — другой процесс может проигнорировать блокировку и писать в файл
- Блокировка привязана к **файлу**, не к FileChannel; если один поток в JVM захватил lock, другой поток в той же JVM не может захватить overlapping lock
- Не все ФС поддерживают (NFS может не поддерживать)

### 5.6. Что такое ScatteringByteChannel и GatheringByteChannel?

Это интерфейсы, расширяющие возможности чтения/записи: за один системный вызов читать в несколько буферов (scatter) или писать из нескольких буферов (gather). `FileChannel`, `SocketChannel` и `DatagramChannel` реализуют оба этих интерфейса.

**Scattering Read** — чтение одного блока данных из канала в несколько буферов последовательно. Полезно, когда у данных фиксированный формат (заголовок + тело):

```java
// Заголовок фиксированной длины (8 байт), потом тело переменной длины
ByteBuffer header = ByteBuffer.allocate(8);
ByteBuffer body = ByteBuffer.allocate(1024);
ByteBuffer[] buffers = { header, body };

SocketChannel channel = ...;
long bytesRead = channel.read(buffers);  // один системный вызов!
// header заполняется первым, потом body
header.flip();
body.flip();
```

**Gathering Write** — запись из нескольких буферов в канал одним системным вызовом. Полезно при сборке ответа из частей:

```java
ByteBuffer header = ByteBuffer.wrap("HTTP/1.1 200 OK\r\n".getBytes());
ByteBuffer body = ByteBuffer.wrap("<html>...</html>".getBytes());
ByteBuffer[] buffers = { header, body };

SocketChannel channel = ...;
channel.write(buffers);  // один системный вызов — header + body вместе
```

**Преимущества:**
- **Меньше системных вызовов:** вместо N вызовов `read(buf)` — один `read(bufs[])`
- **Атомарность на уровне TCP:** gathering write отправляет всё как одно TCP-сообщение (меньше шансов на фрагментацию)
- **Удобство:** не нужно копировать заголовок в общий буфер

---

## 8. Сериализация

### 6.1. Как сериализовать объект в файл (ObjectOutputStream)?

```java
// Класс должен реализовывать java.io.Serializable
class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    // getters, toString…
}

// Сериализация
Person person = new Person("Alice", 30);
try (ObjectOutputStream oos = new ObjectOutputStream(
        new BufferedOutputStream(new FileOutputStream("person.ser")))) {
    oos.writeObject(person);
}

// Десериализация
try (ObjectInputStream ois = new ObjectInputStream(
        new BufferedInputStream(new FileInputStream("person.ser")))) {
    Person restored = (Person) ois.readObject();
    System.out.println(restored);  // Person{name='Alice', age=30}
} catch (ClassNotFoundException e) {
    // Класс не найден в classpath
}
```

**Как работает сериализация внутри:**
1. `ObjectOutputStream` рекурсивно обходит граф объектов через reflection
2. Для каждого объекта записывается: дескриптор класса, `serialVersionUID`, значения non-transient non-static полей
3. Ссылки на уже сериализованные объекты заменяются на «back-reference» (handle) — граф объектов сохраняется корректно
4. При десериализации объект создаётся **без вызова конструктора** (через `Unsafe` или нативный вызов `allocateInstance`)

### 6.2. Что такое transient и зачем он нужен?

`transient` — ключевое слово, указывающее, что поле **не должно быть сериализовано**. При десериализации оно получит значение по умолчанию (null, 0, false).

```java
class User implements Serializable {
    private String username;
    private transient String password;  // не будет сериализовано!

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }
}

User user = new User("alice", "secret");
// После сериализации/десериализации:
// user.username = "alice"
// user.password = null  ← значение по умолчанию
```

**Когда использовать transient:**
- Поля, содержащие конфиденциальные данные (пароли, ключи)
- Вычисляемые поля (кеши, производные значения)
- Ссылки на ресурсы ОС (файловые дескрипторы, соединения с БД)
- Поля, значения которых зависят от контекста JVM/ОС (`Thread`, `InputStream`)
- Отладочные/временные метаданные

### 6.3. Как Serializable влияет на версионирование (serialVersionUID)?

`serialVersionUID` — это уникальный идентификатор версии класса. При десериализации JVM сравнивает `serialVersionUID` сохранённого объекта с `serialVersionUID` текущей версии класса. Если они не совпадают — `InvalidClassException`.

```java
class Person implements Serializable {
    // Без явного serialVersionUID компилятор вычислит его сам
    // на основе: имени класса, имён полей, типов, методов, модификаторов
    private static final long serialVersionUID = 20250712001L;
    // ...
}
```

**Правила версионирования:**
- **Всегда** объявляйте `serialVersionUID` явно
- Если добавили новое поле — увеличьте `serialVersionUID`. Старые данные не прочитаются
- Если поле удалено, но `serialVersionUID` сохранён — при десериализации старое значение игнорируется
- Если поле изменило тип, а `serialVersionUID` сохранён — `ClassCastException` при десериализации

**Как меняется serialVersionUID без явного объявления:**
Компилятор вычисляет хеш (SHA-1) от сигнатуры класса: имени, модификаторов, интерфейсов, полей, методов (кроме private-методов и static-инициализаторов). Любое изменение класса → новый serialVersionUID.

### 6.4. Чем опасна десериализация?

Десериализация — известный вектор атак **Remote Code Execution (RCE)**. Проблема в том, что `readObject()` может выполнить произвольный код, определённый в методе `readObject()` десериализуемого класса.

**Механика атаки (gadget chain):**
Злоумышленник создаёт цепочку объектов (gadget chain), где вызов `readObject()` одного объекта вызывает опасный метод другого, и в итоге выполняется произвольный код (например, `Runtime.exec()`).

```java
// Потенциально опасный класс
class DangerousTask implements Serializable {
    private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
        in.defaultReadObject();
        Runtime.getRuntime().exec("rm -rf /");  // если поле содержит команду
    }
}
```

**Методы защиты:**

```java
// 1. Фильтрация десериализации (Java 9+)
ObjectInputStream ois = new ObjectInputStream(fis);
ois.setObjectInputFilter(info -> {
    if (info.serialClass() != null) {
        // Разрешаем только классы из нашего пакета
        return info.serialClass().getPackageName().startsWith("com.myapp")
            ? ObjectInputFilter.Status.ALLOWED
            : ObjectInputFilter.Status.REJECTED;
    }
    return ObjectInputFilter.Status.UNDECIDED;
});

// 2. Глобальный фильтр (системное свойство или файл конфигурации)
// -Djdk.serialFilter=com.myapp.*;!*

// 3. Использовать альтернативы сериализации:
//    - JSON (Jackson, Gson) — человекочитаемый, но медленнее
//    - Protocol Buffers / gRPC — бинарный, быстрый, схема
//    - Apache Avro — бинарный, компактный
//    - MessagePack — бинарный JSON
```

### 6.5. Как использовать Externalizable вместо Serializable?

`Externalizable` — интерфейс, расширяющий `Serializable` и требующий ручной реализации методов `writeExternal()` и `readExternal()`. Это даёт **полный контроль** над процессом: что и в каком порядке сохранять.

```java
class Person implements Externalizable {
    private String name;
    private int age;

    // ОБЯЗАТЕЛЬНО: public no-arg constructor
    // (Externalizable вызывает конструктор при десериализации)
    public Person() {}

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeUTF(name);
        out.writeInt(age);
        // пароль не пишем — он transient по логике
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = in.readUTF();
        age = in.readInt();
    }
}
```

**Serializable vs Externalizable:**

| Характеристика | Serializable | Externalizable |
|---|---|---|
| Создание объекта | Без конструктора (Unsafe) | Вызывается public no-arg конструктор |
| Контроль | Автоматический (reflection) | Ручной (пишем явно) |
| Производительность | Медленнее (reflection overhead) | Быстрее |
| Размер данных | Больше (метаданные классов, поля) | Меньше (только то, что нужно) |
| Удобство | Просто (implements + маркер) | Больше кода |
| Безопасность | Менее безопасен (автоматическая десериализация) | Безопаснее (явный контроль) |

### 6.6. Как Sealed Classes и Records влияют на сериализацию?

**Records (Java 16+):**
Record — это иммутабельный data-класс, который автоматически реализует `Serializable` (если объявить implements Serializable). При десериализации record вызывает **канонический конструктор**, а не создаётся через Unsafe. Это безопаснее — инварианты, определённые в конструкторе, будут проверены.

```java
record Person(String name, int age) implements Serializable {
    public Person {
        if (age < 0) throw new IllegalArgumentException("age < 0");
        // Этот конструктор будет вызван и при десериализации!
    }
}
```

**Sealed Classes (Java 17+):**
Ограничивают иерархию наследования. При десериализации JVM знает все возможные подклассы, что делает фильтрацию более предсказуемой и уменьшает поверхность для атак с подменой классов:

```java
sealed interface Shape permits Circle, Rectangle { … }
// Объект Shape может быть ТОЛЬКО Circle или Rectangle
// Злоумышленник не сможет подсунуть вредоносный Triangle
```

### 8.7. Что такое readResolve() и writeReplace()? Как защитить синглтоны?

Это специальные методы, которые позволяют классу контролировать **замену объекта** при сериализации/десериализации:

**`writeReplace()`** — вызывается ПЕРЕД сериализацией. Позволяет заменить объект на другой (прокси, сериализационную форму):
```java
class Person implements Serializable {
    private String name;
    private transient SecretData secrets;  // не сериализуем напрямую

    // Вместо Person сериализуем PersonProxy
    private Object writeReplace() {
        return new PersonProxy(name, secrets.encrypt());
    }
}

class PersonProxy implements Serializable {
    private String name;
    private byte[] encryptedSecrets;

    private Object readResolve() {
        return new Person(name, SecretData.decrypt(encryptedSecrets));
    }
}
```

**`readResolve()`** — вызывается ПОСЛЕ десериализации. Позволяет заменить десериализованный объект на другой. Классическое применение — **защита синглтонов**:

```java
// Проблема: десериализация создаёт НОВЫЙ объект синглтона
enum Singleton { INSTANCE }  // Enum — самый надёжный синглтон, Java гарантирует

// Для класса (не enum) нужен readResolve():
class DatabaseConnectionManager implements Serializable {
    private static final DatabaseConnectionManager INSTANCE =
        new DatabaseConnectionManager();

    // Приватный конструктор
    private DatabaseConnectionManager() {
        if (INSTANCE != null) throw new IllegalStateException("Already created");
    }

    public static DatabaseConnectionManager getInstance() {
        return INSTANCE;
    }

    // Защита синглтона при десериализации:
    private Object readResolve() {
        return INSTANCE;  // ВОЗВРАЩАЕМ СУЩЕСТВУЮЩИЙ экземпляр вместо созданного!
    }
}

// Тест:
DatabaseConnectionManager original = DatabaseConnectionManager.getInstance();
byte[] serialized = serialize(original);
DatabaseConnectionManager deserialized = deserialize(serialized);
System.out.println(original == deserialized);  // true — тот же объект!
```

**Важно:** Без `readResolve()` десериализация создаёт новый объект (без вызова конструктора), и синглтон перестаёт быть синглтоном. Но `readResolve()` — не панацея: если атакующий получит доступ к потоку байтов до вызова `readResolve()` (через специально созданный gadget chain), он сможет манипулировать объектом. Enum-синглтоны защищены на уровне JVM — они всегда безопасны.

### 8.8. Как работает ObjectInputFilter (Java 9+) для защиты десериализации?

`ObjectInputFilter` — это фильтр, проверяющий **каждый десериализуемый класс** и принимающий решение: разрешить, запретить или оставить на усмотрение других фильтров.

```java
try (ObjectInputStream ois = new ObjectInputStream(
        new BufferedInputStream(new FileInputStream("data.ser")))) {

    // Фильтр №1: Программный (на конкретный ObjectInputStream)
    ois.setObjectInputFilter(info -> {
        // info.serialClass() — null для массивов и простых типов
        if (info.serialClass() != null) {
            String className = info.serialClass().getName();

            // Разрешаем только классы из нашего пакета
            if (className.startsWith("com.myapp.")) {
                return ObjectInputFilter.Status.ALLOWED;
            }

            // Явный чёрный список известных опасных классов
            Set<String> DANGEROUS = Set.of(
                "org.apache.commons.collections.Transformer",
                "java.lang.Runtime",
                "java.lang.ProcessBuilder"
            );
            if (DANGEROUS.contains(className)) {
                return ObjectInputFilter.Status.REJECTED;
            }

            // Контроль глубины графа объектов и размера массива
            if (info.depth() > 20) {
                System.err.println("Слишком глубокий граф объектов: " + info.depth());
                return ObjectInputFilter.Status.REJECTED;
            }
            if (info.arrayLength() > 10_000_000) {
                System.err.println("Слишком большой массив: " + info.arrayLength());
                return ObjectInputFilter.Status.REJECTED;
            }
            // Поток байт: не более 10 МБ
            if (info.streamBytes() > 10_000_000) {
                return ObjectInputFilter.Status.REJECTED;
            }
        }
        return ObjectInputFilter.Status.UNDECIDED;  // пусть решает глобальный фильтр
    });

    Object obj = ois.readObject();  // каждый класс проходит через фильтр
}
```

**Глобальный фильтр через системные свойства:**

```bash
# Фильтр на уровне JVM: разрешить только com.myapp.*, всё остальное — запретить
java -Djdk.serialFilter="com.myapp.*;!*" MyApp

# Более сложный фильтр: макс. глубина 20, макс. массив 10 МБ, макс. ссылок 1000
java -Djdk.serialFilter="maxdepth=20;maxarray=10000000;maxrefs=1000;com.myapp.*;!*"
```

**Глобальный фильтр через `conf/security/java.security`:**

```
jdk.serialFilter=com.myapp.*;!*
```

**Приоритет фильтров:**
1. Фильтр на `ObjectInputStream` (установлен через `setObjectInputFilter()`)
2. Глобальный фильтр (`jdk.serialFilter`)
3. Если оба вернули `UNDECIDED` → класс разрешён

**Лучшие практики:**
- Всегда настраивайте хотя бы глобальный фильтр на продакшене
- White-list подход (разрешить конкретные пакеты) безопаснее black-list
- Ограничивайте глубину графа, размер массивов и количество ссылок
- Переходите на JSON/Protobuf/Avro для новых проектов — они не подвержены атакам десериализации

---

## 9. Классический сетевой I/O (Socket, ServerSocket)

### 7.1. Как работает Socket и ServerSocket в классическом I/O?

В классической (`java.net`) модели на каждое соединение нужен отдельный поток. Это **блокирующая (blocking)** модель: операция приостанавливает поток до завершения.

```java
// Сервер (классический, однопоточный — плохо!)
try (ServerSocket server = new ServerSocket(8080)) {
    System.out.println("Сервер слушает порт 8080...");
    while (true) {
        // accept() БЛОКИРУЕТСЯ, ожидая клиента
        Socket client = server.accept();
        // Обрабатываем в том же потоке — другие клиенты ждут!
        handleClient(client);
    }
}

// Клиент
try (Socket socket = new Socket("localhost", 8080)) {
    OutputStream out = socket.getOutputStream();
    InputStream in = socket.getInputStream();

    out.write("Hello\n".getBytes());
    out.flush();

    BufferedReader reader = new BufferedReader(new InputStreamReader(in));
    String response = reader.readLine();
    System.out.println("Ответ: " + response);
}
```

**Поток на соединение (thread-per-connection) — чуть лучше, но не масштабируется:**

```java
try (ServerSocket server = new ServerSocket(8080)) {
    while (true) {
        Socket client = server.accept();
        // Каждому клиенту — свой поток (дорого!)
        new Thread(() -> handleClient(client)).start();
    }
}
```

### 7.2. Почему классическая модель плохо масштабируется (проблема C10k)?

Проблема **C10k** (10 000 одновременных соединений) была сформулирована Дэном Кегелем в 1999 году: может ли сервер обрабатывать 10 000 клиентов одновременно?

В модели «один поток на соединение» — **нет**. Причины:

1. **Память:** Каждый платформенный поток имеет стек ~1 МБ. 10 000 потоков = ~10 ГБ только под стеки. Плюс структуры данных ОС на каждый поток.

2. **Переключение контекста:** Планировщик ОС вынужден переключаться между 10 000 потоков. Каждое переключение ~1–10 мкс. На 10 000 потоков, даже если 99% ждут I/O, оставшиеся создают значительный overhead.

3. **Лимиты ОС:** Большинство ОС имеют практический лимит на количество потоков (Linux: ~порядка 10 000, зависит от `pid_max`, памяти; Windows: ~2000–5000).

**Решение:** I/O Multiplexing — один поток управляет тысячами соединений через `Selector` (см. раздел 9). С появлением Virtual Threads (JDK 21) эта проблема решена: можно использовать удобную блокирующую модель с миллионами виртуальных потоков.

---

## 10. NIO — основы (Channel, Buffer, Selector)

### 8.1. Что такое NIO и чем он отличается от классического I/O?

**NIO** (New I/O, появилось в Java 1.4, 2002 г.) — это:
- **Буфер-ориентированный** (Buffer-oriented): данные всегда читаются в буфер и пишутся из буфера
- **Канальный** (Channel-based): каналы двунаправленные, в отличие от однонаправленных потоков
- **Неблокирующий** (Non-blocking): позволяет одному потоку обрабатывать множество соединений через Selector

| Характеристика | Классический I/O (java.io) | NIO (java.nio) |
|---|---|---|
| Абстракция | Поток (Stream) | Канал (Channel) + Буфер (Buffer) |
| Направление | Однонаправленный (in / out) | Двунаправленный |
| Блокировка | Всегда блокирующий | Может быть неблокирующим |
| Мультиплексирование | Нет | Да (Selector) |
| Управление позицией | Только последовательное | Произвольный доступ (FileChannel) |
| Буферизация | Встроенная (Buffered*) | Явная (ByteBuffer) |
| Прямая передача | Нет | Да (transferTo / zero-copy) |
| Memory-mapping | Нет | Да (MappedByteBuffer) |
| Файловые блокировки | Нет | Да (FileLock) |

### 8.2. Какие три основных компонента есть в NIO?

**Channel (Канал):** Транспорт для данных. Как рельсы, по которым едут вагоны с данными. Двунаправленный. Основные реализации:
- `FileChannel` — файлы
- `SocketChannel` — TCP-клиент
- `ServerSocketChannel` — TCP-сервер
- `DatagramChannel` — UDP
- `Pipe.SinkChannel` / `Pipe.SourceChannel` — межпоточный обмен

**Buffer (Буфер):** Контейнер для данных. Как вагон, в котором лежат данные. Данные всегда читаются **в** буфер и пишутся **из** буфера. Основные типы:
- `ByteBuffer` — байты (самый важный)
- `CharBuffer`, `IntBuffer`, `LongBuffer`, `DoubleBuffer`, …

**Selector (Селектор):** Диспетчер, который следит за событиями на нескольких каналах. Позволяет одному потоку управлять тысячами соединений. Сердце мультиплексирования.

### 8.3. Как ByteBuffer работает в NIO?

`ByteBuffer` — это блок памяти с тремя ключевыми указателями:

```
Буфер ёмкостью 10 байт после записи "Hello" (5 байт):

  [H] [e] [l] [l] [o] [ ] [ ] [ ] [ ] [ ]
   0   1   2   3   4   5   6   7   8   9
                       │               │
                   position=5      capacity=10
       │
    limit=10 (до вызова flip)
```

- **`position`** — текущий индекс для чтения/записи. Следующая операция `get()` или `put()` произойдёт здесь
- **`limit`** — первая "запретная" позиция. Нельзя читать/писать за пределами limit
- **`capacity`** — полная ёмкость буфера. Никогда не меняется

**Основные методы управления:**

```java
ByteBuffer buf = ByteBuffer.allocate(1024);   // Heap-буфер, 1024 байта

// Запись (write mode)
buf.put((byte) 1);
buf.put("Hello".getBytes());   // position += 5
buf.putInt(42);                // position += 4

// Переключение в режим чтения
buf.flip();     // limit = position; position = 0

// Чтение (read mode)
byte b = buf.get();            // position += 1
byte[] data = new byte[4];
buf.get(data);                 // position += 4

// Переключение обратно в режим записи (с сохранением непрочитанных данных)
buf.compact();  // копирует непрочитанное в начало; position после данных; limit = capacity

// Полная очистка для переиспользования
buf.clear();    // position = 0; limit = capacity (данные не стираются!)

// Маркировка позиции
buf.mark();     // запомнить position
buf.reset();    // вернуть position к mark
buf.rewind();   // position = 0; limit не меняется
```

```java
// Визуализация переходов:

// 1. Начало (clear())
// pos=0                                        limit=cap=10
// [ _ ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ]

// 2. После put("Hello")
// limit=cap=10                                 pos=5
// [ H ] [ e ] [ l ] [ l ] [ o ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ]

// 3. После flip()
// pos=0                    limit=5              cap=10
// [ H ] [ e ] [ l ] [ l ] [ o ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ]

// 4. После get() × 2
//             pos=2        limit=5              cap=10
// [ H ] [ e ] [ l ] [ l ] [ o ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ]

// 5. После compact()
// pos=3                                limit=cap=10
// [ l ] [ l ] [ o ] [ o ] [ o ] [ _ ] [ _ ] [ _ ] [ _ ] [ _ ]
//  \_________непрочитанные________/
```

### 8.4. Как переключить ByteBuffer между режимами записи и чтения?

Три основных метода:

```java
// flip() — готовимся ЧИТАТЬ то, что только что ЗАПИСАЛИ
buf.flip();  // limit = position; position = 0

// clear() — готовимся ЗАПИСЫВАТЬ заново с начала
buf.clear(); // position = 0; limit = capacity

// compact() — готовимся ЗАПИСЫВАТЬ, но сохраняем непрочитанное
buf.compact(); // копирует [position..limit) в начало; position = оставшееся; limit = capacity
```

**Типичный цикл чтения из канала:**

```java
ByteBuffer buf = ByteBuffer.allocate(1024);

while (channel.read(buf) != -1) {   // читаем в буфер
    buf.flip();                       // переключаем на чтение
    while (buf.hasRemaining()) {      // пока есть данные
        processByte(buf.get());
    }
    buf.clear();                      // готовим к следующему чтению
}
```

### 8.5. Что такое Direct Buffer и чем он отличается от Heap Buffer?

**Heap ByteBuffer** (`ByteBuffer.allocate(n)`):
- Данные хранятся в `byte[]` внутри Java Heap
- GC управляет памятью автоматически
- При I/O операциях данные **копируются** во временный нативный буфер (double copy): Heap → Native → Kernel
- Быстрее создаётся и читается из Java-кода

**Direct ByteBuffer** (`ByteBuffer.allocateDirect(n)`):
- Данные хранятся в нативной памяти (вне Java Heap)
- GC не управляет этой памятью (освобождается через `Cleaner` при сборке объекта)
- При I/O операциях данные передаются напрямую: Native → Kernel (single copy)
- **Медленнее в создании** (системный вызов `malloc`), но **быстрее в I/O**
- Не влияет на размер Java Heap и GC pauses

```java
// Heap buffer — быстро создать, двойное копирование при I/O
ByteBuffer heapBuf = ByteBuffer.allocate(8192);

// Direct buffer — медленнее создать, быстрее I/O
ByteBuffer directBuf = ByteBuffer.allocateDirect(8192);

// Обёртка существующего массива — Heap, без копирования данных
byte[] data = {1, 2, 3, 4, 5};
ByteBuffer wrappedBuf = ByteBuffer.wrap(data);
// wrappedBuf — Heap; изменения в data видны в wrappedBuf и наоборот!
```

**Когда что использовать:**
- **Direct:** долгоживущие буферы для I/O, высокая пропускная способность
- **Heap:** краткосрочные буферы, много операций с данными в Java-коде, тесты
- **MappedByteBuffer:** огромные файлы (ГБ+), случайный доступ

### 8.6. Какие виды Channel существуют?

| Канал | Назначение | Блокирующий? | Неблокирующий? |
|---|---|---|---|
| `FileChannel` | Файлы | Да | Нет (всегда блокирующий) |
| `SocketChannel` | TCP-клиент | Да | Да (`configureBlocking(false)`) |
| `ServerSocketChannel` | TCP-сервер | Да | Да |
| `DatagramChannel` | UDP | Да | Да |
| `Pipe.SinkChannel` | Межпоточная запись | Да | Да |
| `Pipe.SourceChannel` | Межпоточное чтение | Да | Да |
| `AsynchronousFileChannel` | Асинхронная работа с файлами | Асинхронный | Асинхронный |
| `AsynchronousSocketChannel` | Асинхронный TCP | Асинхронный | Асинхронный |

### 8.7. Какой Channel не поддерживает неблокирующий режим?

**`FileChannel`** — он всегда блокирующий. Это особенность большинства операционных систем: **файловые операции всегда блокирующие на уровне ОС**. Даже Linux AIO (libaio) поддерживает асинхронный доступ к файлам только при определённых условиях (O_DIRECT, выровненные буферы). Поэтому для асинхронной работы с файлами в Java есть `AsynchronousFileChannel`, который эмулирует асинхронность через пул потоков.

```java
FileChannel fc = FileChannel.open(Path.of("file.txt"));
// fc.configureBlocking(false);  // ОШИБКА КОМПИЛЯЦИИ! FileChannel не имеет этого метода
```

### 8.8. Что такое неблокирующий режим в NIO?

Неблокирующий режим означает, что I/O операции **возвращают управление немедленно**, даже если данные не готовы:

```java
SocketChannel channel = SocketChannel.open();
channel.configureBlocking(false);   // включаем неблокирующий режим
channel.connect(new InetSocketAddress("example.com", 80));

// В неблокирующем режиме:
int bytesRead = channel.read(buf);  // если данных нет — возвращает 0 (а не блокируется)
if (bytesRead > 0) {
    buf.flip();
    // обрабатываем
}

// connect() тоже неблокирующий:
while (!channel.finishConnect()) {
    // делаем другую полезную работу, пока соединение устанавливается
}
```

**Ключевое отличие от блокирующего режима:**
- Блокирующий: `read()` ждёт, пока появятся данные (поток спит)
- Неблокирующий: `read()` возвращает 0, если данных нет (поток может делать что-то другое)

Это позволяет **одному потоку обслуживать тысячи каналов**, опрашивая их через Selector.

### 8.9. Как SocketChannel используется в неблокирующем режиме?

```java
// Клиент в неблокирующем режиме
SocketChannel client = SocketChannel.open();
client.configureBlocking(false);
client.connect(new InetSocketAddress("example.com", 80));

// Ждём установки соединения
while (!client.finishConnect()) {
    // Можно проверять другие каналы или делать другую работу
    System.out.println("Подключаюсь...");
}

ByteBuffer buf = ByteBuffer.allocate(256);
buf.put("GET / HTTP/1.1\r\nHost: example.com\r\n\r\n".getBytes());
buf.flip();

// Пишем, пока буфер не опустеет
while (buf.hasRemaining()) {
    client.write(buf);
}

// Читаем ответ
buf.clear();
int bytesRead;
while ((bytesRead = client.read(buf)) != -1) {
    if (bytesRead > 0) {
        buf.flip();
        byte[] data = new byte[buf.remaining()];
        buf.get(data);
        System.out.print(new String(data));
        buf.clear();
    }
    // Если bytesRead == 0 — данных пока нет, можем проверить другие каналы
}
	client.close();
```

### 10.10. Как работают slice(), duplicate() и asReadOnlyBuffer() у ByteBuffer?

Эти методы создают **разделяемые подвиды** (shared views) существующего ByteBuffer — они ссылаются на **те же данные**, но имеют собственные `position`, `limit` и `capacity`:

```java
ByteBuffer original = ByteBuffer.allocate(10);
original.put(new byte[]{0, 1, 2, 3, 4, 5, 6, 7, 8, 9});
original.flip();  // position=0, limit=10

// ----- slice() — буфер на [position, limit) -----
original.position(3);
ByteBuffer slice = original.slice();  // разделяет данные с позиции 3 до limit(10)
// slice: position=0, limit=7, capacity=7
// slice.get(0) = original.get(3) = 3

slice.put(0, (byte) 99);  // меняем в slice → меняется и в original!
System.out.println(original.get(3));  // 99 — одни и те же данные

// ----- duplicate() — полная копия метаданных -----
original.position(0);  // возвращаем позицию
ByteBuffer dup = original.duplicate();
// dup: position=0, limit=10, capacity=10 — независимые указатели, общие данные
dup.put(0, (byte) 77);
System.out.println(original.get(0));  // 77

// ----- asReadOnlyBuffer() — защита от записи -----
ByteBuffer readOnly = original.asReadOnlyBuffer();
readOnly.get(0);   // OK
// readOnly.put(0, (byte) 88);  // ❌ ReadOnlyBufferException!
```

**Сравнение методов:**

| Метод | Данные | position | limit | capacity | Запись |
|---|---|---|---|---|---|
| `slice()` | Общие, с позиции `position()` | 0 | `remaining()` | `remaining()` | Да |
| `duplicate()` | Общие, весь буфер | Копия `position()` | Копия `limit()` | Копия `capacity()` | Да |
| `asReadOnlyBuffer()` | Общие, весь буфер | Копия `position()` | Копия `limit()` | Копия `capacity()` | **Нет** |

**Практический пример: парсинг сетевого пакета без копирования данных:**

```java
// Получили пакет: [header 8 байт] [body N байт] [footer 4 байта]
ByteBuffer packet = ByteBuffer.allocate(1024);
// ... channel.read(packet);
packet.flip();

// Выделяем части без копирования:
packet.limit(8);           // первые 8 байт — заголовок
ByteBuffer header = packet.slice();  // header ссылается на байты 0-7

packet.limit(packet.capacity()); // восстанавливаем
packet.position(8);
packet.limit(packet.limit() - 4);  // от 8 до (конец-4) — тело
ByteBuffer body = packet.slice();   // body — без копирования!

packet.position(packet.limit());
packet.limit(packet.capacity());    // последние 4 байта — footer
ByteBuffer footer = packet.slice();

// Теперь работаем с header, body, footer независимо:
int msgType = header.getInt(0);
int msgLen = header.getInt(4);

// Миксуем прочитанные части с безопасным only-read:
ByteBuffer safeBody = body.asReadOnlyBuffer();  // обработчик не испортит данные
handler.process(safeBody);
```

### 10.11. Что такое ByteOrder (Big-Endian vs Little-Endian) в ByteBuffer?

`ByteOrder` определяет, в каком порядке байты многобайтовых типов (`int`, `long`, `double`, …) хранятся в буфере:

- **Big-Endian (BE):** старший байт по младшему адресу (сетевой порядок, Java по умолчанию)
- **Little-Endian (LE):** младший байт по младшему адресу (порядок x86/x64 процессоров)

```java
ByteBuffer buf = ByteBuffer.allocate(4);

// Big-Endian (по умолчанию в Java):
buf.order(ByteOrder.BIG_ENDIAN);
buf.putInt(0, 0x01020304);
// Байты: [01] [02] [03] [04] — старший байт 01 по индексу 0
System.out.printf("BE: %02X %02X %02X %02X%n",
    buf.get(0), buf.get(1), buf.get(2), buf.get(3));  // 01 02 03 04

// Little-Endian:
buf.order(ByteOrder.LITTLE_ENDIAN);
buf.putInt(0, 0x01020304);
// Байты: [04] [03] [02] [01] — младший байт 04 по индексу 0
System.out.printf("LE: %02X %02X %02X %02X%n",
    buf.get(0), buf.get(1), buf.get(2), buf.get(3));  // 04 03 02 01

// Узнать текущий порядок:
System.out.println("Текущий: " + buf.order());  // LITTLE_ENDIAN

// Нативный порядок процессора:
System.out.println("Нативный: " + ByteOrder.nativeOrder());  // LITTLE_ENDIAN на x86
```

**Когда это важно:**
- **Сетевые протоколы:** почти всегда Big-Endian (network byte order)
- **Файловые форматы:** зависит от формата (JPEG — Big-Endian, BMP — Little-Endian)
- **Межплатформенный обмен:** нужно договориться о порядке (Protobuf использует LE)
- **Производительность:** нативный порядок (обычно LE) работает быстрее, так как не требует перестановки байтов

```java
// Когда читаете сетевые данные — всегда Big-Endian:
buf.order(ByteOrder.BIG_ENDIAN);
int port = buf.getInt();  // читаем как BE

// Для локального файла — нативный порядок быстрее:
buf.order(ByteOrder.nativeOrder());
buf.putInt(value);
```

---

## 11. Мультиплексирование и Selector (Reactor Pattern)

### 9.1. Как работает Selector в NIO?

`Selector` — это реализация паттерна **Reactor**. Он позволяет одному потоку следить за множеством каналов и обрабатывать только те, на которых произошли события (пришли данные, завершено соединение, …).

**Жизненный цикл Selector:**

```
1. Создание:           Selector.open()
2. Регистрация канала: channel.register(selector, SelectionKey.OP_READ)
3. Ожидание событий:   selector.select() — блокируется до событий
4. Обработка ключей:   Set<SelectionKey> keys = selector.selectedKeys()
5. Итерация:           для каждого ключа → обработать → удалить из selectedKeys
6. Повтор:             вернуться к шагу 3
```

```java
Selector selector = Selector.open();

// Регистрируем ServerSocketChannel для приёма соединений
ServerSocketChannel serverChannel = ServerSocketChannel.open();
serverChannel.bind(new InetSocketAddress(8080));
serverChannel.configureBlocking(false);
serverChannel.register(selector, SelectionKey.OP_ACCEPT);

while (true) {
    selector.select();  // БЛОКИРУЕМСЯ до событий на любом зарегистрированном канале

    Set<SelectionKey> selectedKeys = selector.selectedKeys();
    Iterator<SelectionKey> iter = selectedKeys.iterator();

    while (iter.hasNext()) {
        SelectionKey key = iter.next();

        if (key.isAcceptable()) {
            // Новое входящее соединение
            ServerSocketChannel server = (ServerSocketChannel) key.channel();
            SocketChannel client = server.accept();
            client.configureBlocking(false);
            client.register(selector, SelectionKey.OP_READ);
        }
        else if (key.isReadable()) {
            // Данные готовы к чтению
            SocketChannel client = (SocketChannel) key.channel();
            ByteBuffer buf = ByteBuffer.allocate(256);
            int read = client.read(buf);
            if (read == -1) {  // соединение закрыто
                client.close();
            } else if (read > 0) {
                buf.flip();
                // обрабатываем данные
            }
        }

        iter.remove();  // ВАЖНО: удалить обработанный ключ
    }
}
```

### 9.2. Как Selector помогает в мультиплексировании соединений?

Мультиплексирование — возможность одного потока обслуживать множество каналов. Selector позволяет потоку «спать» на методе `select()` и просыпаться **только тогда, когда где-то произошло событие** (пришли данные, можно писать, новое соединение).

**Модель «один поток — несколько каналов»:**

```
Один поток с Selector:
  ├─ Канал 1: OP_READ готов → читаем
  ├─ Канал 2: OP_WRITE готов → пишем
  ├─ Канал 3: ожидание
  ├─ ...
  └─ Канал 10 000: ожидание
```

**Сравнение с классической моделью:**

| Модель | Потоков на 10 000 клиентов | Память на стеки | Переключений контекста |
|---|---|---|---|
| thread-per-connection | 10 000 | ~10 ГБ | Десятки тысяч/сек |
| NIO + Selector (1 поток) | 1 | ~1 МБ | Минимум |
| NIO + Selector (N потоков = ядрам CPU) | 4–8 | ~4–8 МБ | Минимум |

### 9.3. Как реализовать простой NIO-сервер с ServerSocketChannel и Selector?

```java
public class NioEchoServer {
    public static void main(String[] args) throws IOException {
        Selector selector = Selector.open();

        // Серверный канал
        ServerSocketChannel serverChannel = ServerSocketChannel.open();
        serverChannel.bind(new InetSocketAddress(8080));
        serverChannel.configureBlocking(false);
        serverChannel.register(selector, SelectionKey.OP_ACCEPT);

        System.out.println("Echo сервер запущен на порту 8080");

        while (true) {
            selector.select();  // ждём события

            for (Iterator<SelectionKey> it = selector.selectedKeys().iterator(); it.hasNext(); ) {
                SelectionKey key = it.next();
                it.remove();

                if (!key.isValid()) continue;

                if (key.isAcceptable()) {
                    // Принимаем новое соединение
                    ServerSocketChannel ssc = (ServerSocketChannel) key.channel();
                    SocketChannel client = ssc.accept();
                    client.configureBlocking(false);
                    client.register(selector, SelectionKey.OP_READ);
                    System.out.println("Подключился: " + client.getRemoteAddress());
                }
                else if (key.isReadable()) {
                    // Читаем данные
                    SocketChannel client = (SocketChannel) key.channel();
                    ByteBuffer buf = ByteBuffer.allocate(1024);

                    try {
                        int bytesRead = client.read(buf);
                        if (bytesRead == -1) {
                            // Клиент закрыл соединение
                            System.out.println("Отключился: " + client.getRemoteAddress());
                            client.close();
                            continue;
                        }
                        if (bytesRead > 0) {
                            buf.flip();
                            // Echo: отправляем обратно то, что получили
                            client.write(buf);
                        }
                    } catch (IOException e) {
                        // Обрыв соединения
                        client.close();
                    }
                }
            }
        }
    }
}
```

### 9.4. Что такое SelectionKey и какие операции можно регистрировать?

`SelectionKey` представляет **регистрацию канала в селекторе**. Он хранит:
- Канал (`channel()`)
- Селектор (`selector()`)
- Интересующие операции (interest set)
- Готовые операции (ready set)
- Аттачмент (произвольный объект, `attach()` / `attachment()`)

**Операции (готовность канала):**

| Константа | Что означает | Для каких каналов |
|---|---|---|
| `OP_ACCEPT` | Готов принять новое соединение | `ServerSocketChannel` |
| `OP_CONNECT` | Соединение установлено | `SocketChannel` (клиент) |
| `OP_READ` | Данные готовы к чтению | `SocketChannel`, `Pipe.SourceChannel`, `DatagramChannel` |
| `OP_WRITE` | Можно писать данные | `SocketChannel`, `Pipe.SinkChannel`, `DatagramChannel` |

```java
// Регистрация с несколькими операциями
channel.register(selector, SelectionKey.OP_READ | SelectionKey.OP_WRITE);

// Аттачмент — удобно хранить контекст соединения
class ClientContext {
    ByteBuffer readBuffer = ByteBuffer.allocate(1024);
    ByteBuffer writeBuffer;
    // ...
}
channel.register(selector, SelectionKey.OP_READ, new ClientContext());

// Позже:
ClientContext ctx = (ClientContext) key.attachment();
```

**Важно об OP_WRITE:** Канал почти всегда готов к записи (пока буфер сокета не заполнен). Если зарегистрировать `OP_WRITE` сразу, `select()` будет возвращать управление постоянно (busy loop). Правильный подход: регистрировать `OP_WRITE` только когда есть данные для отправки, и снимать после записи:

```java
// Правильный паттерн:
// 1. Когда хотим писать — регистрируем OP_WRITE
key.interestOps(key.interestOps() | SelectionKey.OP_WRITE);

// 2. В цикле обработки:
if (key.isWritable()) {
    SocketChannel ch = (SocketChannel) key.channel();
    ch.write(writeBuffer);
    if (!writeBuffer.hasRemaining()) {
        // Всё записали — снимаем OP_WRITE
        key.interestOps(key.interestOps() & ~SelectionKey.OP_WRITE);
    }
}
```

---

## 12. Платформенно-зависимые механизмы мультиплексирования (epoll, kqueue, IOCP)

### 10.1. Как Java использует epoll на Linux?

**epoll** (event poll) — это системный вызов Linux (ядро 2.6+, 2002 г.) для мультиплексирования I/O. Это самый эффективный механизм для обслуживания тысяч файловых дескрипторов. Java использует epoll через класс `EPollSelectorProvider` (внутренний, в пакете `sun.nio.ch`).

**API epoll (C):**
```c
int epfd = epoll_create1(0);            // создать epoll instance
epoll_ctl(epfd, EPOLL_CTL_ADD, fd, &ev); // добавить дескриптор
epoll_wait(epfd, events, MAX_EVENTS, timeout); // ждать события
```

**Как это связано с Java Selector:**

Когда вы вызываете `Selector.open()` на Linux, создаётся `EPollSelectorImpl`, который внутри вызывает `epoll_create1()`. Каждая регистрация канала через `channel.register(selector, ops)` вызывает `epoll_ctl(EPOLL_CTL_ADD)`. Вызов `selector.select()` транслируется в `epoll_wait()`.

```java
// Java-код (одинаков на всех платформах)
Selector selector = Selector.open();  // На Linux: EPollSelectorImpl
serverChannel.register(selector, OP_ACCEPT);
selector.select();  // На Linux: epoll_wait()
```

**Преимущества epoll перед select/poll:**
- **O(1)** по количеству дескрипторов (select/poll — O(n), проходят весь список)
- **Неограниченное количество дескрипторов** (select ограничен `FD_SETSIZE`, обычно 1024)
- **Edge-triggered режим** (см. 10.4)
- **epoll_ctl изменяет только указанный дескриптор** (poll требует пересборки всего массива каждый раз)

### 10.2. Что такое kqueue и как Java использует его на macOS/BSD?

**kqueue** — механизм мультиплексирования в macOS, FreeBSD, OpenBSD и других BSD-системах. Аналог epoll в мире BSD. Java использует kqueue через `KQueueSelectorProvider` (также внутренний).

```c
// API kqueue (C)
int kq = kqueue();                            // создать очередь
EV_SET(&ev, fd, EVFILT_READ, EV_ADD, 0, 0, NULL); // настроить событие
kevent(kq, &ev, 1, NULL, 0, NULL);             // зарегистрировать
kevent(kq, NULL, 0, events, MAX_EVENTS, &timeout); // ждать событий
```

**Отличия kqueue от epoll:**
- kqueue более универсален: может следить не только за I/O, но и за процессами, сигналами, таймерами, изменениями ФС (аналог inotify)
- API kqueue более элегантен (одна функция `kevent` для регистрации и ожидания)
- kqueue поддерживает edge-triggered и level-triggered режимы

### 10.3. Как Java использует IOCP на Windows?

**IOCP** (I/O Completion Ports) — это механизм асинхронного I/O в Windows. В отличие от epoll/kqueue, которые являются механизмами **мультиплексирования с уведомлением о готовности**, IOCP — это истинный **асинхронный I/O** (уведомление о завершении).

Java использует IOCP двумя способами:
1. **`WindowsSelectorImpl`** (для `Selector`) — эмулирует готовность через IOCP, вызывая асинхронные операции и ожидая их завершения
2. **`WindowsAsynchronousSocketChannel`** и **`WindowsAsynchronousFileChannel`** — используют IOCP напрямую для истинно асинхронного I/O

На Windows `AsynchronousFileChannel` действительно асинхронный (использует IOCP), в отличие от Linux, где асинхронность эмулируется через пул потоков.

### 10.4. Edge-triggered vs Level-triggered — что использует Java?

**Level-triggered (LT, по уровню):**
- Событие будет сообщаться **каждый раз**, пока данные доступны
- Если прочитали не всё — при следующем `select()` снова получим уведомление
- Проще в использовании, но может вызывать лишние пробуждения

**Edge-triggered (ET, по фронту):**
- Событие будет сообщено **только один раз** при изменении состояния
- Если прочитали не всё — следующего уведомления **не будет**, пока не придут новые данные
- Эффективнее (меньше пробуждений), но требует читать до упора (до EAGAIN)

**Java NIO Selector использует Level-triggered по умолчанию.** Это сделано для простоты использования и совместимости кода между платформами.

```java
// В level-triggered режиме (Java): если не прочитали все данные,
// следующий select() снова вернёт этот канал как OP_READ
selector.select();
for (SelectionKey key : selector.selectedKeys()) {
    if (key.isReadable()) {
        channel.read(buf);  // прочитали только часть
        // На следующем select() снова получим этот канал — данные ещё есть
    }
}
```

### 10.5. Как SelectorProvider выбирает реализацию?

`SelectorProvider` — это абстрактный класс, который создаёт платформенно-зависимые реализации `Selector`, `ServerSocketChannel`, `SocketChannel` и т.д.

**Как выбирается провайдер (в порядке приоритета):**
1. Системное свойство `java.nio.channels.spi.SelectorProvider` (если задано — загружается указанный класс)
2. Сервис-провайдер через SPI (файл `META-INF/services/java.nio.channels.spi.SelectorProvider`)
3. Платформенный провайдер по умолчанию:
   - **Linux:** `sun.nio.ch.EPollSelectorProvider`
   - **macOS/BSD:** `sun.nio.ch.KQueueSelectorProvider`
   - **Windows:** `sun.nio.ch.WindowsSelectorProvider`
   - **Solaris:** `sun.nio.ch.DevPollSelectorProvider`

```java
// Узнать текущую реализацию (косвенно):
Selector selector = Selector.open();
System.out.println(selector.getClass().getName());
// На Linux: sun.nio.ch.EPollSelectorImpl
// На macOS: sun.nio.ch.KQueueSelectorImpl
```

### 10.6. Какие проблемы были с epoll в JDK и как их исправляли (epoll bug, JDK 21)?

**Проблема «epoll bug» (JDK до 21):**

В Linux есть известная проблема: когда TCP-соединение разрывается (RST) до того, как Java успела его прочитать через `SelectableChannel`, epoll может сообщить о событии `EPOLLHUP`, но Java `Selector` не обрабатывает его корректно. Результат: **бесконечный цикл** — `select()` немедленно возвращает управление (spinning) с пустым набором ключей, загружая CPU на 100%.

**Обходные решения (до JDK 21):**
- Пересоздание Selector при обнаружении spinning
- Использование таймаутов в `select(timeout)`
- Периодическая отмена регистрации и повторная регистрация каналов

**JDK 21: фундаментальное исправление (JEP 453/JEP 444 — Virtual Threads)**

С JDK 21, когда виртуальный поток выполняет блокирующий системный вызов (например, `socket.read()`), JVM заменяет блокирующую операцию на неблокирующую + подписку через epoll. Виртуальный поток размонтируется с платформенного, и JVM ждёт события epoll для возобновления. Это значит, что **код epoll теперь поддерживается самой JVM на глубоком уровне**, а не только через NIO Selector API.

Кроме того, в JDK 21 был переписан внутренний код `EPollSelectorImpl` для более корректной обработки событий `EPOLLHUP` и `EPOLLERR`.

**JDK 24: синхронизированный epoll в Virtual Threads (JEP 491)**

До JDK 24 виртуальный поток не мог размонтироваться внутри `synchronized` блока (pinning). Это означало, что если виртуальный поток вызывает `socket.read()` внутри `synchronized`, он блокирует платформенный поток — и epoll-оптимизация не работает. JDK 24 устраняет это ограничение: теперь виртуальные потоки могут размонтироваться даже внутри `synchronized` блоков, что делает epoll-интеграцию полностью прозрачной.

### 12.7. Что такое io_uring и будет ли он в Java?

**io_uring** (Linux 5.1+, 2019) — это новейший механизм асинхронного I/O в Linux, который решает фундаментальные проблемы предыдущих подходов:

**Проблемы, которые решает io_uring:**
- **epoll** — только уведомления о готовности, само чтение/запись всё ещё требуют системных вызовов
- **AIO (libaio)** — работает только с `O_DIRECT`, требует выровненных буферов, ненадёжен
- **io_uring** — истинный асинхронный I/O: и уведомление, и передача данных происходят асинхронно

**Как работает io_uring:**
```
Пользовательское пространство (Java):
  Submission Queue (SQ) — помещаем заявки на I/O операции
  Completion Queue (CQ) — забираем готовые результаты

Ядро Linux:
  Читает SQ → выполняет операции → помещает результаты в CQ

Ключевое: обе очереди разделяются между Userspace и Kernelspace (shared memory),
          что позволяет избежать системных вызовов при интенсивном I/O!
```

**API io_uring (C, упрощённо):**
```c
// Настройка
int ring_fd = io_uring_setup(ENTRIES, &params);

// Получаем отображённые в память очереди SQ и CQ
void *sq_ptr = mmap(..., ring_fd, IORING_OFF_SQ_RING);
void *cq_ptr = mmap(..., ring_fd, IORING_OFF_CQ_RING);

// Помещаем операцию в SQ, ядро само прочитает
io_uring_get_sqe(ring);  // получаем слот в SQ
io_uring_prep_read(sqe, fd, buf, size, offset);  // заполняем: ЧИТАТЬ
io_uring_submit(ring);   // сообщаем ядру: есть новые операции

// Забираем результат из CQ
io_uring_wait_cqe(ring, &cqe);  // ждём завершения
// cqe.res = количество прочитанных байт (или ошибка)
```

**Текущий статус в Java:** На середину 2026 года io_uring **не поддерживается** в JDK напрямую. Однако:
- **Project Loom** (Virtual Threads) использует io_uring под капотом для реализации блокирующих операций в виртуальных потоках на Linux (начиная с JDK 21 для определённых операций)
- **Project Panama** (Foreign Function & Memory API) позволяет взаимодействовать с io_uring из Java через JNI-подобные вызовы без нативного кода
- Ведутся обсуждения о добавлении `IouringSelectorProvider` как прямой замены `EPollSelectorProvider`

**Почему io_uring важен для Java:**
1. **Меньше системных вызовов:** shared-memory очереди вместо `epoll_wait()` + `read()`
2. **Истинная асинхронность для файлов:** в отличие от `AsynchronousFileChannel`, который эмулирует асинхронность через пул потоков
3. **Батчинг операций:** можно отправить сразу много I/O-операций одной командой
4. **Будущее высокопроизводительных Java-приложений:** особенно для СУБД, файловых серверов, прокси

**Пример использования io_uring через Project Panama (экспериментально):**
```java
// На данный момент (JDK 26) — только через FFM API и ручное управление,
// прямая поддержка io_uring ожидается в будущих версиях JDK.
// Следите за JEP-ами, связанными с io_uring.
```

---

## 13. NIO Pipe и DatagramChannel

### 11.1. Что такое Pipe в NIO и для чего он нужен?

`Pipe` — это однонаправленная труба для передачи данных между потоками внутри одной JVM. Состоит из двух каналов:
- **`Pipe.SourceChannel`** — чтение (аналог `PipedInputStream`)
- **`Pipe.SinkChannel`** — запись (аналог `PipedOutputStream`)

```java
Pipe pipe = Pipe.open();

// Поток-писатель
new Thread(() -> {
    try {
        Pipe.SinkChannel sinkChannel = pipe.sink();
        ByteBuffer buf = ByteBuffer.wrap("Hello from pipe!".getBytes());
        sinkChannel.write(buf);
        System.out.println("Записано в pipe");
    } catch (IOException e) { /* ... */ }
}).start();

// Поток-читатель (main)
Pipe.SourceChannel sourceChannel = pipe.source();
ByteBuffer buf = ByteBuffer.allocate(128);
int bytesRead = sourceChannel.read(buf);
buf.flip();
System.out.println("Прочитано из pipe: " +
    new String(buf.array(), 0, buf.remaining()));
```

**Отличия Pipe от PipedInputStream/PipedOutputStream:**
- Pipe работает через NIO Channel/Buffer — можно использовать в неблокирующем режиме
- Pipe можно зарегистрировать в Selector (для SourceChannel) — вписать в общий event loop
- Pipe обычно быстрее на больших объёмах данных

### 11.2. Что такое DatagramChannel?

`DatagramChannel` — канал для работы с UDP (User Datagram Protocol). В отличие от TCP (`SocketChannel`):
- **Без установки соединения** — данные отправляются дейтаграммами
- **Нет гарантии доставки** — пакеты могут теряться, дублироваться, менять порядок
- **Быстрее TCP** — нет overhead на установку соединения, подтверждения, контроль потока
- **Широковещательные и multicast-рассылки**

```java
// Сервер
DatagramChannel server = DatagramChannel.open();
server.bind(new InetSocketAddress(9999));
server.configureBlocking(false);  // можно в неблокирующем

ByteBuffer buf = ByteBuffer.allocate(1024);
while (true) {
    buf.clear();
    SocketAddress clientAddr = server.receive(buf);  // получаем дейтаграмму
    buf.flip();

    byte[] data = new byte[buf.remaining()];
    buf.get(data);
    System.out.println("Получено от " + clientAddr + ": " + new String(data));

    // Ответ
    buf.rewind();
    server.send(buf, clientAddr);
}

// Клиент
DatagramChannel client = DatagramChannel.open();
ByteBuffer buf = ByteBuffer.wrap("Hello UDP".getBytes());
client.send(buf, new InetSocketAddress("localhost", 9999));
```

**Когда использовать UDP (DatagramChannel):**
- Потоковое видео/аудио (потери не критичны)
- Онлайн-игры (скорость важнее надёжности)
- DNS-запросы
- Сетевое обнаружение (service discovery, multicast)
- Логирование с высокой пропускной способностью

---

## 14. Асинхронный I/O (AsynchronousChannel)

### 12.1. Что такое AsynchronousFileChannel и зачем он нужен?

`AsynchronousFileChannel` (NIO.2, Java 7) — канал для асинхронного чтения/записи файлов. Вы запускаете операцию (например, прочитать 100 МБ) и **продолжаете выполнение программы**, а о завершении узнаёте через `Future` или `CompletionHandler`.

**Зачем это нужно, если FileChannel всегда блокирующий?** Да, на большинстве ОС файловые операции синхронны. `AsynchronousFileChannel` эмулирует асинхронность через пул потоков: операция выполняется в отдельном потоке, а ваш код продолжает работу.

```java
// Открытие
AsynchronousFileChannel channel = AsynchronousFileChannel.open(
        Path.of("large.dat"), StandardOpenOption.READ);

ByteBuffer buf = ByteBuffer.allocate(1024 * 1024);  // 1 МБ

// Асинхронное чтение (Future)
Future<Integer> future = channel.read(buf, 0);  // читаем с позиции 0
System.out.println("Чтение запущено, делаем другую работу...");

doOtherWork();  // параллельная работа

// Ждём завершения
int bytesRead = future.get();  // блокируется до завершения
System.out.println("Прочитано: " + bytesRead + " байт");
```

### 12.2. Как открыть файл в асинхронном режиме?

```java
// Простое открытие (пул потоков по умолчанию)
AsynchronousFileChannel channel = AsynchronousFileChannel.open(
        Path.of("file.txt"),
        StandardOpenOption.READ,
        StandardOpenOption.WRITE);

// С пользовательским ExecutorService
ExecutorService executor = Executors.newFixedThreadPool(4);
AsynchronousFileChannel channel = AsynchronousFileChannel.open(
        Path.of("file.txt"),
        Set.of(StandardOpenOption.READ, StandardOpenOption.WRITE),
        executor);  // свой пул потоков
```

### 12.3. Какие операции поддерживает AsynchronousFileChannel?

| Операция | Сигнатура | Описание |
|---|---|---|
| `read` | `Future<Integer> read(ByteBuffer, long pos)` | Чтение с указанной позиции |
| `write` | `Future<Integer> write(ByteBuffer, long pos)` | Запись на указанную позицию |
| `lock` | `Future<FileLock> lock()` | Блокировка файла |
| `force` | `void force(boolean metaData)` | Сброс на диск (синхронный) |
| `size` | `long size()` | Размер файла (синхронный) |
| `truncate` | `AsynchronousFileChannel truncate(long)` | Обрезать файл (синхронный) |

**Важно:** `force()`, `size()` и `truncate()` — синхронные методы (не имеют асинхронных версий).

### 12.4. Как обработать результат асинхронной операции (Future vs CompletionHandler)?

**Способ 1: Future (проще, но нужно ждать)**

```java
Future<Integer> future = channel.read(buf, 0);

// Можно проверить, не завершилась ли операция
if (future.isDone()) {
    int bytesRead = future.get();
}

// Или задать таймаут
int bytesRead = future.get(5, TimeUnit.SECONDS);
```

**Способ 2: CompletionHandler (более эффективный, callback-style)**

```java
channel.read(buf, 0, null, new CompletionHandler<Integer, Void>() {
    @Override
    public void completed(Integer bytesRead, Void attachment) {
        System.out.println("Прочитано " + bytesRead + " байт");
        buf.flip();
        // обработка данных
    }

    @Override
    public void failed(Throwable exc, Void attachment) {
        System.err.println("Ошибка чтения: " + exc.getMessage());
        exc.printStackTrace();
    }
});

// Главный поток не блокируется — он продолжает работу
System.out.println("Чтение выполняется асинхронно...");
Thread.sleep(5000);  // ждём для демонстрации
```

**Сравнение:**

| Характеристика | Future | CompletionHandler |
|---|---|---|
| Стиль | Блокирующее ожидание (poll или get) | Callback |
| Простота | Проще для начинающих | Требует понимания обратных вызовов |
| Эффективность | Менее эффективен (нужен поток для ожидания) | Более эффективен (callback в пуле потоков) |
| Композиция | Можно комбинировать с CompletableFuture | Сложнее комбинировать |
| Обработка ошибок | Через `ExecutionException` при `get()` | Явный метод `failed()` |

### 12.5. Какой пул потоков используется по умолчанию для асинхронных операций? Можно ли указать свой?

**По умолчанию:** Системный пул потоков, управляемый через `AsynchronousChannelGroup`. Для каждого такого канала по умолчанию создаётся группа с кешируемым пулом потоков.

**Можно указать свой пул:**

```java
// Создаём группу с фиксированным пулом
ExecutorService executor = Executors.newFixedThreadPool(8);
AsynchronousChannelGroup group = AsynchronousChannelGroup.withThreadPool(executor);

// Открываем канал с этой группой
AsynchronousFileChannel channel = AsynchronousFileChannel.open(
        Path.of("file.dat"), Set.of(StandardOpenOption.READ), group);

// Или передаём executor напрямую
AsynchronousFileChannel channel2 = AsynchronousFileChannel.open(
        Path.of("file.dat"), Set.of(StandardOpenOption.READ), executor);

// При завершении — shutdown группы
group.shutdown();
```

### 12.6. Что такое AsynchronousSocketChannel и как реализовать асинхронный I/O?

`AsynchronousSocketChannel` — асинхронный TCP-канал (NIO.2). В отличие от `SocketChannel` с Selector, здесь операции возвращают `Future` или принимают `CompletionHandler`.

```java
// Асинхронный сервер
AsynchronousServerSocketChannel server = AsynchronousServerSocketChannel.open()
        .bind(new InetSocketAddress(8080));

System.out.println("Асинхронный сервер на порту 8080");

// Принимаем соединения асинхронно
server.accept(null, new CompletionHandler<AsynchronousSocketChannel, Void>() {
    @Override
    public void completed(AsynchronousSocketChannel client, Void attachment) {
        System.out.println("Подключился: " + client);

        // Сразу принимаем следующее соединение
        server.accept(null, this);

        // Читаем от клиента асинхронно
        ByteBuffer buf = ByteBuffer.allocate(1024);
        client.read(buf, null, new CompletionHandler<Integer, Void>() {
            @Override
            public void completed(Integer bytesRead, Void att) {
                if (bytesRead > 0) {
                    buf.flip();
                    client.write(buf, null, new CompletionHandler<>() {
                        @Override
                        public void completed(Integer result, Void att) {
                            try { client.close(); } catch (IOException e) {}
                        }
                        @Override
                        public void failed(Throwable exc, Void att) {}
                    });
                }
            }
            @Override
            public void failed(Throwable exc, Void att) {
                try { client.close(); } catch (IOException e) {}
            }
        });
    }

    @Override
    public void failed(Throwable exc, Void attachment) {
        System.err.println("Ошибка accept: " + exc);
    }
});

// Держим main-поток
Thread.currentThread().join();
```

**Когда использовать AsynchronousSocketChannel vs Selector:**
- `AsynchronousSocketChannel` хорош для простых сценариев с малым количеством соединений и сложной логикой обработки каждого
- `Selector` предпочтительнее для высоконагруженных серверов (прокси, message brokers) — меньше overhead на callback'и
- С JDK 21+ Virtual Threads делают оба подхода менее актуальными для большинства случаев

### 12.7. Как дождаться завершения всех асинхронных операций?

Есть несколько способов:

```java
// Способ 1: CountDownLatch (простой и надёжный)
int totalOps = 10;
CountDownLatch latch = new CountDownLatch(totalOps);

for (int i = 0; i < totalOps; i++) {
    ByteBuffer buf = ByteBuffer.allocate(1024);
    channel.read(buf, i * 1024, null, new CompletionHandler<Integer, Void>() {
        @Override
        public void completed(Integer result, Void attachment) {
            System.out.println("Операция завершена: " + result);
            latch.countDown();
        }
        @Override
        public void failed(Throwable exc, Void attachment) {
            exc.printStackTrace();
            latch.countDown();  // всё равно уменьшаем счётчик!
        }
    });
}

latch.await();  // ждём завершения всех операций
System.out.println("Все операции завершены");

// Способ 2: Собрать все Future и ждать
List<Future<Integer>> futures = new ArrayList<>();
for (int i = 0; i < totalOps; i++) {
    futures.add(channel.read(ByteBuffer.allocate(1024), i * 1024));
}
for (Future<Integer> f : futures) {
    f.get();  // блокируется до завершения каждой
}

// Способ 3: CompletableFuture.allOf
CompletableFuture<?>[] cfs = futures.stream()
    .map(f -> CompletableFuture.supplyAsync(() -> {
        try { return f.get(); } catch (Exception e) { throw new RuntimeException(e); }
    }))
    .toArray(CompletableFuture[]::new);
CompletableFuture.allOf(cfs).join();
```

### 12.8. Какие исключения могут возникнуть при асинхронных операциях?

При использовании **Future:**
- `ExecutionException` при вызове `future.get()` — оборачивает реальную причину
- `InterruptedException` при `future.get()` — если поток прерван во время ожидания
- `TimeoutException` при `future.get(timeout, unit)` — если операция не завершилась за указанное время
- `CancellationException` — если `future.cancel()` был вызван до завершения

При использовании **CompletionHandler:**
- Исключение передаётся в метод `failed(Throwable exc, Void attachment)`
- Это может быть `IOException`, `NonWritableChannelException`, `NonReadableChannelException`, `ClosedChannelException` и др.

```java
// Обработка ошибок в CompletionHandler
channel.read(buf, 0, null, new CompletionHandler<Integer, Void>() {
    @Override
    public void completed(Integer result, Void attachment) {
        // успех
    }

    @Override
    public void failed(Throwable exc, Void attachment) {
        if (exc instanceof ClosedChannelException) {
            System.err.println("Канал уже закрыт");
        } else if (exc instanceof NonReadableChannelException) {
            System.err.println("Канал не открыт для чтения");
        } else if (exc instanceof IOException) {
            System.err.println("Ошибка I/O: " + exc.getMessage());
        } else {
            System.err.println("Неизвестная ошибка: " + exc);
        }
        // Логирование, fallback, повтор…
    }
});
```

### 12.9. Как избежать утечек памяти при работе с AsynchronousFileChannel?

1. **Всегда закрывайте канал:** `channel.close()`. Незакрытый канал удерживает нативные ресурсы и потоки в пуле.

2. **Не удерживайте ByteBuffer дольше необходимого:** Если операция долгая, а буфер большой — он висит в памяти, пока операция не завершится.

3. **Следите за пулом потоков:** Если вы создали свой `ExecutorService` — не забудьте вызвать `shutdown()`:

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
try (AsynchronousFileChannel channel = AsynchronousFileChannel.open(
        path, Set.of(READ), executor)) {
    // работаем
} finally {
    executor.shutdown();  // иначе потоки останутся висеть
}
```

4. **При большом количестве асинхронных операций** контролируйте их количество (back-pressure), чтобы не исчерпать память:

```java
// Ограничение через семафор
Semaphore semaphore = new Semaphore(100);  // не более 100 одновременных операций

for (int i = 0; i < 10_000; i++) {
    semaphore.acquire();  // ждём свободный слот
    channel.read(buf, i * 4096, null, new CompletionHandler<>() {
        @Override
        public void completed(Integer result, Void att) {
            semaphore.release();  // освобождаем слот
        }
        @Override
        public void failed(Throwable exc, Void att) {
            semaphore.release();  // освобождаем слот даже при ошибке
        }
    });
}
```

### 12.10. В каких сценариях AsynchronousFileChannel эффективнее синхронного I/O?

- **Много одновременных операций с разными файлами** — параллельное чтение снижает общее время
- **Операции чередуются с вычислениями** — пока читается файл, CPU занят обработкой предыдущих данных
- **Высоконагруженные веб-серверы** — отдача статических файлов асинхронно
- **Сложная бизнес-логика после чтения** — callback-модель хорошо ложится на асинхронные фреймворки

**Когда НЕ стоит использовать:**
- Одно файловое чтение подряд (нет выигрыша от асинхронности)
- Простые скрипты и batch-обработка (синхронный код проще)
- С JDK 21+ можно использовать Virtual Threads + синхронный FileChannel (проще, почти та же производительность)

---

## 15. Работа с ZIP-архивами

### 13.1. Что такое ZipInputStream и ZipOutputStream?

- **`ZipInputStream`** — поток для чтения данных из ZIP-архива. Позволяет читать архив, не распаковывая его полностью на диск.
- **`ZipOutputStream`** — поток для создания ZIP-архивов, добавляя в него файлы (ZipEntry).

```java
// Создание ZIP-архива
try (ZipOutputStream zos = new ZipOutputStream(
        new BufferedOutputStream(new FileOutputStream("archive.zip")))) {

    // Уровень сжатия: 0 (без) … 9 (макс)
    zos.setLevel(Deflater.BEST_COMPRESSION);

    // Добавляем файл
    ZipEntry entry = new ZipEntry("folder/hello.txt");
    zos.putNextEntry(entry);
    zos.write("Hello from ZIP!".getBytes(StandardCharsets.UTF_8));
    zos.closeEntry();

    // Добавляем ещё файл
    ZipEntry entry2 = new ZipEntry("data.bin");
    entry2.setTime(System.currentTimeMillis());  // метка времени
    zos.putNextEntry(entry2);
    Files.copy(Path.of("data.bin"), zos);
    zos.closeEntry();
}
```

### 13.2. Как прочитать содержимое ZIP-архива с помощью ZipInputStream?

```java
try (ZipInputStream zis = new ZipInputStream(
        new BufferedInputStream(new FileInputStream("archive.zip")))) {

    ZipEntry entry;
    while ((entry = zis.getNextEntry()) != null) {
        System.out.println("Читаю: " + entry.getName());

        if (entry.isDirectory()) {
            System.out.println("  → директория, пропускаем");
            zis.closeEntry();
            continue;
        }

        // Читаем содержимое entry
        ByteArrayOutputStream baos = new ByteArrayOutputStream();
        byte[] buffer = new byte[8192];
        int read;
        while ((read = zis.read(buffer)) != -1) {
            baos.write(buffer, 0, read);
        }

        System.out.println("  Размер: " + baos.size() + " байт");
        zis.closeEntry();
    }
}
```

### 13.3. Как получить список файлов в ZIP-архиве без распаковки?

```java
// Способ 1: ZipInputStream (последовательно, без загрузки в память)
try (ZipInputStream zis = new ZipInputStream(
        new BufferedInputStream(new FileInputStream("archive.zip")))) {
    ZipEntry entry;
    while ((entry = zis.getNextEntry()) != null) {
        System.out.printf("%s (%,d байт, сжато: %,d)%n",
                entry.getName(), entry.getSize(), entry.getCompressedSize());
        zis.closeEntry();
    }
}

// Способ 2: ZipFile (есть random access, но загружает центральную директорию)
try (ZipFile zipFile = new ZipFile("archive.zip")) {
    zipFile.stream()
            .map(entry -> String.format("%s (%,d байт)", entry.getName(), entry.getSize()))
            .forEach(System.out::println);
}
```

### 13.4. Как распаковать ZIP-архив в указанную директорию?

```java
public static void unzip(Path zipPath, Path destDir) throws IOException {
    Files.createDirectories(destDir);
    Path destDirReal = destDir.toRealPath();  // для проверок безопасности

    try (ZipInputStream zis = new ZipInputStream(
            new BufferedInputStream(Files.newInputStream(zipPath)))) {

        ZipEntry entry;
        while ((entry = zis.getNextEntry()) != null) {
            Path outputPath = destDirReal.resolve(entry.getName()).normalize();

            // Защита от Zip Slip
            if (!outputPath.startsWith(destDirReal)) {
                throw new SecurityException("Zip Slip detected: " + entry.getName());
            }

            if (entry.isDirectory()) {
                Files.createDirectories(outputPath);
            } else {
                Files.createDirectories(outputPath.getParent());
                Files.copy(zis, outputPath, StandardCopyOption.REPLACE_EXISTING);
            }
            zis.closeEntry();
        }
    }
}
```

### 13.5. Что такое ZipFile и чем он отличается от ZipInputStream?

`ZipFile` — класс, открывающий ZIP-архив для **произвольного доступа** (random access). Он читает центральную директорию архива (таблицу всех файлов в конце ZIP) и позволяет читать любой файл по имени.

```java
try (ZipFile zipFile = new ZipFile("archive.zip")) {
    // Произвольный доступ по имени
    ZipEntry entry = zipFile.getEntry("folder/hello.txt");
    if (entry != null) {
        try (InputStream in = zipFile.getInputStream(entry)) {
            String content = new String(in.readAllBytes(), StandardCharsets.UTF_8);
            System.out.println(content);
        }
    }
}
```

**ZipFile vs ZipInputStream:**

| Характеристика | ZipFile | ZipInputStream |
|---|---|---|
| Доступ | Произвольный (по имени) | Только последовательный |
| Память | Загружает центральную директорию (~размер списка файлов) | Не загружает |
| Скорость поиска | O(log n) или O(n) по центральной директории | Нужно пройти весь архив |
| Когда использовать | Нужен доступ к конкретному файлу | Обработка всех файлов подряд, стриминг |

### 13.6. Как проверить, что файл является ZIP-архивом?

```java
// Способ 1: Проверка "магического числа" (первые 4 байта)
public static boolean isZipFile(Path path) throws IOException {
    try (InputStream in = Files.newInputStream(path)) {
        byte[] magic = new byte[4];
        if (in.read(magic) != 4) return false;
        // ZIP magic: 0x50 0x4B 0x03 0x04 ("PK\003\004")
        return magic[0] == 0x50 && magic[1] == 0x4B
            && magic[2] == 0x03 && magic[3] == 0x04;
    }
}

// Способ 2: Попробовать открыть ZipFile
public static boolean isZipFileSafe(Path path) {
    try (ZipFile zip = new ZipFile(path.toFile())) {
        return true;
    } catch (IOException e) {
        return false;
    }
}
```

### 13.7. Как обработать вложенные (nested) ZIP-архивы?

Когда `ZipEntry` сам является ZIP-архивом, нужно обернуть текущий поток в новый `ZipInputStream`, но **не закрывать** основной поток:

```java
try (ZipInputStream outer = new ZipInputStream(
        new BufferedInputStream(Files.newInputStream(Path.of("outer.zip"))))) {
    ZipEntry entry;
    while ((entry = outer.getNextEntry()) != null) {
        if (entry.getName().endsWith(".zip")) {
            System.out.println("Найден вложенный ZIP: " + entry.getName());
            // Создаём новый ZIS, НЕ закрывая outer!
            ZipInputStream inner = new ZipInputStream(outer);  // outer — это поток
            try {
                ZipEntry innerEntry;
                while ((innerEntry = inner.getNextEntry()) != null) {
                    System.out.println("  Внутри: " + innerEntry.getName());
                    // читаем innerEntry...
                    inner.closeEntry();
                }
            } finally {
                // inner.close() НЕ закрывает outer! (историческая особенность)
                // Но лучше не полагаться и закрыть вручную
            }
        }
        outer.closeEntry();
    }
}
```

### 13.8. Как обрабатывать пароли и шифрование в ZIP?

**Стандартный JDK не поддерживает зашифрованные ZIP-файлы.** Ни `ZipInputStream`, ни `ZipFile` не умеют работать с паролями (ни с традиционным ZipCrypto, ни с AES).

```java
// Для запароленных ZIP нужна сторонняя библиотека — Zip4j
// Зависимость: net.lingala.zip4j:zip4j:2.11.5

import net.lingala.zip4j.ZipFile;

// Чтение запароленного архива
try (ZipFile zipFile = new ZipFile("encrypted.zip", "password".toCharArray())) {
    zipFile.extractAll("/output/dir");
}

// Создание запароленного архива с AES
try (ZipFile zipFile = new ZipFile("encrypted.zip", "password".toCharArray())) {
    net.lingala.zip4j.model.ZipParameters params = new net.lingala.zip4j.model.ZipParameters();
    params.setEncryptFiles(true);
    params.setEncryptionMethod(EncryptionMethod.AES);  // AES, а не ZipCrypto
    zipFile.addFile(new File("secret.txt"), params);
}
```

### 13.9. Что такое Zip Slip и как от него защититься?

**Zip Slip** — атака, при которой злоумышленник создаёт ZIP-архив, где имя файла (`ZipEntry.getName()`) содержит `../` для выхода за пределы целевой директории. При распаковке такой архив может перезаписать системные файлы (например, `../../.ssh/authorized_keys`).

```java
// ❌ Уязвимый код
Path destDir = Path.of("/safe/uploads");
try (ZipInputStream zis = ...) {
    ZipEntry entry;
    while ((entry = zis.getNextEntry()) != null) {
        // ОПАСНО: прямой resolve без проверки
        Path outPath = destDir.resolve(entry.getName());
        Files.copy(zis, outPath);  // может записать в /etc/passwd!
    }
}

// ✅ Защищённый код
Path destDirReal = destDir.toRealPath();  // канонический путь
while ((entry = zis.getNextEntry()) != null) {
    Path outPath = destDirReal.resolve(entry.getName()).normalize();
    if (!outPath.startsWith(destDirReal)) {
        throw new SecurityException("Zip Slip: " + entry.getName());
    }
    Files.createDirectories(outPath.getParent());
    Files.copy(zis, outPath);
}
```

### 13.10. Как ZipInputStream обрабатывает большие файлы (>4 ГБ, ZIP64)?

Java поддерживает формат **ZIP64** (расширение оригинального ZIP, снимающее ограничения 4 ГБ на размер файла и 65 535 на количество файлов). `ZipInputStream` и `ZipFile` прозрачно обрабатывают ZIP64-архивы.

```java
// ZIP64 работает из коробки — никаких специальных действий
try (ZipFile zip = new ZipFile("huge.zip")) {
    ZipEntry entry = zip.getEntry("bigfile.dat");
    System.out.println("Размер: " + entry.getSize());  // может быть > 4 ГБ
    // getSize() возвращает long — поддерживает большие файлы
}
```

---

## 16. RandomAccessFile

### 14.1. Что такое RandomAccessFile и чем он отличается от FileInputStream/FileOutputStream?

`RandomAccessFile` — класс для чтения **и** записи файлов с произвольным доступом. Он ведёт себя как большой массив байтов на диске с курсором (file pointer). В отличие от потоков, RAF не наследуется ни от `InputStream`, ни от `OutputStream`.

**Отличия:**
- Двунаправленный — и читает, и пишет через один объект
- Произвольный доступ через `seek()` — можно перепрыгнуть в любую позицию
- Знает свою позицию через `getFilePointer()`
- Поддерживает синхронный режим записи (rws/rwd)

```java
// Открытие для чтения и записи
try (RandomAccessFile raf = new RandomAccessFile("data.bin", "rw")) {
    raf.writeInt(42);           // пишем int (4 байта)
    raf.writeDouble(3.14);      // пишем double (8 байт)

    raf.seek(0);                // возвращаемся в начало
    int i = raf.readInt();      // читаем int: 42
    double d = raf.readDouble(); // читаем double: 3.14

    long pos = raf.getFilePointer();  // текущая позиция: 12
    long len = raf.length();          // размер файла
}
```

### 14.2. Какие режимы открытия файла поддерживает RandomAccessFile?

| Режим | Чтение | Запись | Синхронизация | Описание |
|---|---|---|---|---|
| `"r"` | ✅ | ❌ | — | Только чтение. Если файла нет → `FileNotFoundException` |
| `"rw"` | ✅ | ✅ | Нет | Чтение и запись. Файл создаётся, если не существует |
| `"rws"` | ✅ | ✅ | Данные + метаданные | Каждая запись синхронно сбрасывается на диск (данные + метаданные) |
| `"rwd"` | ✅ | ✅ | Только данные | Каждая запись синхронно сбрасывается на диск (только данные) |

```java
// "rw" — обычный, не гарантирует синхронную запись
RandomAccessFile raf = new RandomAccessFile("file.dat", "rw");

// "rws" — каждая write() сразу на диск (медленнее, но надёжнее)
RandomAccessFile rafSync = new RandomAccessFile("critical.dat", "rws");

// "r" — только чтение
RandomAccessFile rafRead = new RandomAccessFile("file.dat", "r");
```

### 14.3. Как перемещаться по файлу с помощью seek() и узнать текущую позицию?

```java
try (RandomAccessFile raf = new RandomAccessFile("data.bin", "r")) {
    long fileSize = raf.length();

    // Переместиться на позицию 100 (в байтах от начала)
    raf.seek(100);
    System.out.println("Позиция: " + raf.getFilePointer());  // 100

    // Переместиться в конец файла
    raf.seek(fileSize);

    // Переместиться на позицию, кратную 1024
    raf.seek(5 * 1024);  // 5120

    // Пропустить N байт вперёд (альтернатива seek)
    raf.skipBytes(200);  // переместиться на 200 байт вперёд от текущей позиции
}
```

**Важно:** `seek()` не проверяет границы. Если указать позицию за концом файла, то при чтении будет `EOFException`, а при записи файл **расширится** (образуется "дыра" из нулевых байтов).

### 14.4. Как читать/писать примитивные типы (readInt, writeDouble) и строки?

```java
try (RandomAccessFile raf = new RandomAccessFile("types.bin", "rw")) {
    // Запись примитивов (Big-Endian, как в DataOutputStream)
    raf.writeBoolean(true);     // 1 байт
    raf.writeByte(127);         // 1 байт
    raf.writeShort(32000);      // 2 байта
    raf.writeChar('A');         // 2 байта
    raf.writeInt(1_000_000);    // 4 байта
    raf.writeLong(1_000_000_000_000L);  // 8 байт
    raf.writeFloat(3.14f);      // 4 байта
    raf.writeDouble(2.71828);   // 8 байт

    // Запись строк
    raf.writeUTF("Привет");  // модифицированный UTF-8 (длина + байты)

    // Чтение в том же порядке
    raf.seek(0);  // возвращаемся в начало
    boolean b = raf.readBoolean();
    byte bt = raf.readByte();
    short s = raf.readShort();
    char c = raf.readChar();
    int i = raf.readInt();
    long l = raf.readLong();
    float f = raf.readFloat();
    double d = raf.readDouble();
    String str = raf.readUTF();
}
```

**Чтение строк с произвольными кодировками (не UTF):**

```java
// readLine() — только ISO-8859-1, устарел!
// Правильный способ: читать байты и декодировать вручную
byte[] buf = new byte[1024];
int read = raf.read(buf);
String text = new String(buf, 0, read, StandardCharsets.UTF_8);

// Или прочитать фиксированное количество байт
byte[] fixedBuf = new byte[256];
raf.readFully(fixedBuf);  // гарантированно читает 256 байт (или EOFException)
```

### 14.5. Как редактировать файл в середине, не перезаписывая его полностью?

**Короткий ответ:** только если новые данные **точно такой же длины**, что и старые. Файловые системы не поддерживают «вставку» байтов в середину файла.

```java
try (RandomAccessFile raf = new RandomAccessFile("config.dat", "rw")) {
    // Читаем запись в позиции 1024
    raf.seek(1024);
    int value = raf.readInt();  // старое значение

    // Меняем на новое (ровно 4 байта — та же длина)
    raf.seek(1024);
    raf.writeInt(value * 2);    // перезаписали на том же месте
}
```

**Если длина меняется** — нужно сдвигать весь «хвост» файла:
- Скопировать остаток файла (от позиции вставки до конца) во временный буфер
- Записать новые данные
- Дописать сохранённый остаток
- Обрезать файл (`setLength()`), если новые данные короче

Это медленно и опасно при сбоях. Для таких задач лучше использовать базу данных.

### 14.6. Как реализовать простую БД на основе RandomAccessFile?

Используя **записи фиксированной длины**. Тогда позицию записи N можно вычислить как `N * RECORD_SIZE`:

```java
class Record {
    static final int RECORD_SIZE = 256;  // фиксированный размер записи

    int id;
    String name;  // макс 120 байт в UTF-8
    int age;

    void write(RandomAccessFile raf) throws IOException {
        raf.writeInt(id);           // 4 байта
        // Имя: фиксированная длина
        byte[] nameBytes = name.getBytes(StandardCharsets.UTF_8);
        raf.write(nameBytes, 0, Math.min(nameBytes.length, 240));
        // Дополняем нулями до фикс. размера
        for (int i = nameBytes.length; i < 240; i++) {
            raf.writeByte(0);
        }
        raf.writeInt(age);          // 4 байта
        // Итого: 4 + 240 + 4 = 248 (оставляем запас)
    }

    void read(RandomAccessFile raf) throws IOException {
        id = raf.readInt();
        byte[] nameBytes = new byte[240];
        raf.readFully(nameBytes);
        name = new String(nameBytes, StandardCharsets.UTF_8).trim();  // обрезаем \0
        age = raf.readInt();
    }
}

// Использование
try (RandomAccessFile db = new RandomAccessFile("database.dat", "rw")) {
    Record r = new Record();
    r.id = 1; r.name = "Alice"; r.age = 30;

    // Запись рекорда #5
    db.seek(5L * Record.RECORD_SIZE);
    r.write(db);

    // Чтение рекорда #5
    db.seek(5L * Record.RECORD_SIZE);
    r.read(db);
    System.out.println(r.id + ": " + r.name + ", " + r.age);
}
```

### 14.7. В чём разница между режимами "rws" и "rwd"?

Оба режима гарантируют синхронную запись (каждый `write()` немедленно на диск), но отличаются областью синхронизации:

- **`"rwd"`** (Read Write Data sync): гарантирует, что **байты файла** записаны на диск. Метаданные (время модификации, размер) могут не обновляться синхронно. Меньше операций I/O → быстрее.

- **`"rws"`** (Read Write Sync): гарантирует запись **байтов + метаданных** (время изменения, права доступа и т.д.). Медленнее, так как требует дополнительной записи метаданных.

```java
// "rwd" — только данные синхронно (быстрее)
try (RandomAccessFile raf = new RandomAccessFile("journal.log", "rwd")) {
    raf.writeBytes("log entry\n");
    // Данные на диске, но mtime может не обновиться
}

// "rws" — данные и метаданные синхронно (медленнее, но полная гарантия)
try (RandomAccessFile raf = new RandomAccessFile("critical.db", "rws")) {
    raf.writeInt(importantValue);
    // И данные, и метаданные гарантированно на диске
}
```

**Аналоги в NIO:** `StandardOpenOption.SYNC` (аналог rws) и `StandardOpenOption.DSYNC` (аналог rwd).

### 14.8. Почему RandomAccessFile медленнее, чем FileChannel + ByteBuffer? Как ускорить?

**Причины медленности RandomAccessFile:**
1. Каждый `read()`/`write()` — это системный вызов (дорого)
2. Нет буферизации по умолчанию
3. Использует старые нативные вызовы, менее оптимизированные
4. Нет zero-copy, memory-mapping

**Как ускорить:**

1. **Использовать большие буферы** — читать/писать массивами, а не побайтово:
```java
byte[] buf = new byte[65536];
int read = raf.read(buf);  // один системный вызов на 64 КБ
```

2. **Получить FileChannel из RandomAccessFile:**
```java
RandomAccessFile raf = new RandomAccessFile("file", "rw");
FileChannel channel = raf.getChannel();
// Теперь можно использовать все преимущества FileChannel:
MappedByteBuffer buf = channel.map(READ_WRITE, 0, channel.size());
// Или channel.transferTo(...)
```

3. **Использовать MappedByteBuffer для больших файлов:**
```java
try (RandomAccessFile raf = new RandomAccessFile("huge.dat", "rw")) {
    MappedByteBuffer buf = raf.getChannel().map(READ_WRITE, 0, raf.length());
    // Читаем/пишем напрямую в память — ОС сама управляет подгрузкой страниц
    int value = buf.getInt(1024);
    buf.putInt(1024, value * 2);
}
```

### 14.9. RandomAccessFile vs FileChannel — что когда использовать?

| Сценарий | Что выбрать |
|---|---|
| Простое последовательное чтение/запись | FileInputStream/FileOutputStream + буферизация |
| Произвольный доступ к небольшим файлам | RandomAccessFile (проще API) |
| Произвольный доступ к большим файлам | FileChannel + MappedByteBuffer |
| Высокопроизводительное копирование | FileChannel.transferTo/transferFrom |
| Блокировка файла между процессами | FileChannel.lock() |
| Записи фиксированной длины (простая БД) | RandomAccessFile (удобно: seek, readInt, writeInt) |
| Асинхронная работа с файлами | AsynchronousFileChannel |

---

## 17. Virtual Threads и I/O (JDK 21+)

### 15.1. Как Virtual Threads меняют модель I/O в Java?

**До Virtual Threads:**
- Блокирующий I/O прост в написании, но требует поток на соединение → проблема C10k
- NIO + Selector решает C10k, но код сложнее (callback hell, явные буферы)
- Программист должен выбирать: простой код или масштабируемость

**С Virtual Threads (JDK 21+):**
- Можно писать **простой блокирующий код** («один поток на соединение»)
- Под капотом JVM делает его **неблокирующим**: когда виртуальный поток вызывает `socket.read()`, он размонтируется с платформенного потока, и ОС ждёт данные через epoll
- **Миллионы виртуальных потоков** на тысячах платформенных

```java
// До JDK 21: нужен NIO Selector для масштабирования (сложно)

// JDK 21+: простой блокирующий код, но масштабируется!
try (ServerSocket server = new ServerSocket(8080)) {
    while (true) {
        Socket client = server.accept();
        Thread.ofVirtual().start(() -> {
            try (client) {
                BufferedReader in = new BufferedReader(
                        new InputStreamReader(client.getInputStream()));
                PrintWriter out = new PrintWriter(client.getOutputStream(), true);

                String line;
                while ((line = in.readLine()) != null) {
                    out.println("Echo: " + line);
                }
            } catch (IOException e) { /* ... */ }
        });
    }
}
// Этот код обработает миллионы соединений — как NIO, но с простотой java.io!
```

### 15.2. Что такое pinning виртуальных потоков и как JDK 24 решает эту проблему?

**До JDK 24:** Если виртуальный поток вызывает блокирующую операцию **внутри `synchronized` блока или метода**, он **не может размонтироваться** с платформенного потока (pinning). Платформенный поток блокируется, и все виртуальные потоки, которые могли бы на нём работать, ждут.

```java
// До JDK 24 — ПРОБЛЕМА:
synchronized (lock) {           // <-- виртуальный поток прикреплён (pinned)
    socket.read();               // <-- БЛОКИРУЕТ платформенный поток!
}
// Платформенный поток заблокирован до выхода из synchronized
```

**JDK 24 (JEP 491):** `synchronized` больше не pin-ит виртуальные потоки. JVM может размонтировать виртуальный поток даже внутри synchronized-блока:

```java
// JDK 24+ — РЕШЕНО:
synchronized (lock) {           // <-- виртуальный поток НЕ прикреплён
    socket.read();               // <-- JVM размонтирует поток, не блокируя платформенный
}
// Платформенный поток свободен для других виртуальных потоков
```

**Что это значит для I/O:** Теперь **любой** код, использующий `synchronized`, может безопасно работать в виртуальных потоках без риска исчерпания платформенных потоков. Это устраняет последнее препятствие для повсеместного использования виртуальных потоков.

### 15.3. Нужен ли NIO/Selector при использовании Virtual Threads?

**Короткий ответ:** В большинстве случаев — нет.

Причина: Virtual Threads решают ту же проблему (масштабирование I/O), но с гораздо более простой моделью программирования. Вместо реактивного кода с коллбеками — обычный синхронный код.

**Когда NIO/Selector всё ещё нужен:**
- Высокопроизводительные сетевые прокси (Netty и подобные фреймворки оптимизированы до предела)
- Работа с существующим кодом на NIO
- Специфические сценарии с жёсткими требованиями по latency (GC паузы)
- На JDK < 21

**Когда выбрать Virtual Threads:**
- Типичные веб-приложения, REST API, микросервисы
- Обработка запросов к БД, брокерам сообщений
- Любой код, где вам нужна простота синхронного I/O

### 15.4. Как Structured Concurrency (JEP 480) связано с I/O?

**Structured Concurrency** (JEP 480, preview в JDK 21, стабилизировано в JDK 24) — это подход к управлению конкурентными задачами, где время жизни подзадач ограничено временем жизни родительской задачи (как в блочных конструкциях языка).

В контексте I/O, Structured Concurrency позволяет запускать несколько параллельных I/O-операций и гарантировать их завершение при выходе из блока:

```java
// Параллельная загрузка из нескольких источников
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    Future<String> user = scope.fork(() -> fetchFromAPI("/user"));
    Future<String> orders = scope.fork(() -> fetchFromAPI("/orders"));
    Future<String> products = scope.fork(() -> fetchFromAPI("/products"));

    scope.join();           // ждём завершения всех подзадач
    scope.throwIfFailed();  // пробрасываем исключение, если любая задача упала

    // Все результаты готовы — собираем ответ
    String response = combine(user.resultNow(), orders.resultNow(), products.resultNow());
}
// scope.close() гарантирует завершение всех подзадач
```

Это особенно полезно с Virtual Threads: каждый `fork()` запускает новый виртуальный поток (дёшево!), а structured подход гарантирует корректное завершение всех I/O-операций.

---

## 18. Модели ввода-вывода — сравнительный анализ

### 16.1. Blocking I/O (блокирующий ввод-вывод)

Поток делает системный вызов `read()` и **блокируется** до тех пор, пока данные не станут доступны. Всё это время поток не может делать ничего другого.

```
Поток: read(fd, buf, size)
   │
   ├── Kernel: ждём данные от диска/сети
   │       │
   │       ├── Данные готовы
   │       │
   ├── Kernel: копируем данные Kernel → User (buf)
   │
   └── Поток продолжает работу
```

**Плюсы:**
- Простейшая модель программирования
- Понятная обработка ошибок
- Подходит для простых приложений

**Минусы:**
- Поток ничего не делает, пока ждёт данные
- Нужен поток на каждое соединение → проблема C10k
- Много потоков → много памяти и переключений контекста

**Java:** `FileInputStream.read()`, `Socket.read()`, `ServerSocket.accept()`

### 16.2. Non-blocking I/O (неблокирующий ввод-вывод)

Поток делает системный вызов `read()` и **немедленно получает ответ**: либо есть данные, либо нет (EAGAIN/EWOULDBLOCK). Поток может опрашивать несколько сокетов по очереди (polling).

```
Поток: read(fd1, buf, size) → -1, EAGAIN (нет данных)
Поток: read(fd2, buf, size) → -1, EAGAIN
Поток: read(fd3, buf, size) → 42 (есть данные!)
// потратили CPU на холостые опросы fd1 и fd2
```

**Плюсы:**
- Один поток может обслуживать много соединений
- Не блокируется

**Минусы:**
- **Busy-waiting** — активный опрос сжигает CPU, если данных нет
- Сложнее программировать (нужно обрабатывать частичные чтения)

**Java:** `SocketChannel.configureBlocking(false)`

### 16.3. I/O Multiplexing (мультиплексирование — select/poll/epoll)

Поток передаёт **список файловых дескрипторов** в системный вызов (`select`, `poll`, `epoll`) и **блокируется до тех пор, пока хотя бы один не станет готов**. Когда возвращается управление, поток знает, какие дескрипторы готовы, и обрабатывает только их.

```
Поток: multiplexer.wait({fd1, fd2, fd3, ..., fd10000})
   │
   ├── Kernel: ждём события на любом из 10000 дескрипторов
   │       │
   │       ├── fd42 готов к чтению!
   │
   └── Поток: обрабатываем только fd42
```

**Плюсы:**
- Один поток обслуживает тысячи соединений без холостого опроса
- Меньше системных вызовов (один `epoll_wait` вместо тысяч `read`)
- Масштабируется на десятки тысяч соединений

**Минусы:**
- Сложнее программировать (событийно-ориентированный код)
- Нужно управлять буферами для каждого соединения
- `select`/`poll` имеют ограничения (FD_SETSIZE, линейная сложность)

**Java:** `Selector` (реализация: epoll на Linux, kqueue на macOS, IOCP на Windows)

### 16.4. Asynchronous I/O (асинхронный ввод-вывод)

Поток инициирует операцию `read()` и **сразу продолжает работу**. Когда ядро завершит операцию (данные готовы **и** скопированы в пользовательский буфер), оно уведомляет поток через callback или сигнал.

```
Поток: aio_read(fd, buf, size, callback)
   │
   └── Поток продолжает работу немедленно

... (поток делает другие дела) ...

Kernel: данные готовы, скопированы в buf
   │
   └── Kernel: вызывает callback(data)
```

**Плюсы:**
- Максимальная эффективность — поток вообще не ждёт I/O
- Идеально для throughput-ориентированных систем

**Минусы:**
- Самая сложная модель программирования (callback hell)
- На большинстве ОС файловые операции не поддерживают настоящий AIO
- Сложная обработка ошибок

**Java:** `AsynchronousFileChannel`, `AsynchronousSocketChannel` (NIO.2)

### 16.5. Сравнительная таблица всех моделей

| Характеристика | Blocking | Non-blocking | Multiplexing | Async |
|---|---|---|---|---|
| Поток блокируется? | Да | Нет | Да (на select) | Нет |
| Инициатор ожидания | Поток (read) | Поток (poll) | Поток (select) | Kernel (callback) |
| Масштабируемость | Низкая (1 поток/соед.) | Низкая (busy-wait) | Высокая (100K+) | Высокая |
| Сложность кода | Простая | Средняя | Высокая | Очень высокая |
| Поддержка в Java | java.io, java.net | NIO (configureBlocking) | NIO Selector | NIO.2 AsyncChannel |
| Реализация в ОС | read() | read() + O_NONBLOCK | select/poll/epoll/kqueue | IOCP (Win), AIO (Linux) |

### 16.6. Какую модель когда выбирать?

| Сценарий | Модель | Почему |
|---|---|---|
| CLI-утилиты, скрипты, прототипы | Blocking | Простота важнее производительности |
| Простое веб-приложение (до 1K соединений) | Blocking (с Virtual Threads JDK 21+) | Лучшее из обоих миров |
| Высоконагруженный HTTP API (10K–1M соединений) | JDK 21+: Blocking + Virtual Threads; JDK <21: Multiplexing (Netty) | Масштабируемость |
| Сетевой прокси, API Gateway | Multiplexing (Netty, NIO Selector) | Нативный zero-copy, минимальный overhead |
| Файловый сервер, CDN | Zero-copy (transferTo) + Async | Прямая передача файлов, высокая пропускная способность |
| Реактивные системы (RxJava, Project Reactor) | Async (AsynchronousChannel) | Естественное продолжение реактивного стиля |
| Микросервисы (JDK 21+) | Blocking + Virtual Threads + Structured Concurrency | Простой код, отличная масштабируемость |

---

## 19. Безопасность ввода-вывода

### 19.1. Что такое TOCTOU (Time-of-check to time-of-use) и как защищаться?

**TOCTOU** (Time-Of-Check to Time-Of-Use) — это класс уязвимостей, когда между проверкой условия и использованием ресурса проходит время, за которое противник может изменить состояние системы:

```java
// ❌ Уязвимый код (TOCTOU):
Path path = Path.of("/tmp/user_upload");

// Шаг 1: ПРОВЕРКА — файл существует?
if (Files.exists(path)) {
    // ⏱️ В этот момент злоумышленник может удалить файл и создать символическую ссылку на /etc/passwd!

    // Шаг 2: ИСПОЛЬЗОВАНИЕ
    String content = Files.readString(path);  // читаем /etc/passwd вместо файла пользователя!
}
```

**Методы защиты:**

**1. Использовать атомарные операции NIO.2:**

```java
// ✅ Правильно: открываем файл И проверяем за одну операцию
try (InputStream in = Files.newInputStream(path)) {
    // Если файла нет или нет прав — исключение, атомарно
    // ...
} catch (NoSuchFileException e) {
    // Файла нет
} catch (AccessDeniedException e) {
    // Нет прав
}

// ✅ Правильно: используем Files.write() с CREATE_NEW
try {
    Files.write(path, data, StandardOpenOption.CREATE_NEW);  // атомарно!
    // Если файл внезапно появился → FileAlreadyExistsException
} catch (FileAlreadyExistsException e) {
    // Кто-то создал файл между проверкой и записью
}
```

**2. Проверять дескриптор, а не путь:**

```java
// ✅ Проверяем реальный файл (по дескриптору), а не путь:
try (FileChannel channel = FileChannel.open(path, READ)) {
    FileLock lock = channel.lock();  // блокируем файл

    // Сравниваем файловый ключ (inode), а не путь
    Object fileKey = Files.readAttributes(path, BasicFileAttributes.class).fileKey();
    if (!expectedKey.equals(fileKey)) {
        throw new SecurityException("Файл подменили!");
    }
    // Теперь безопасно работаем с channel
}
```

**3. Использовать FileStore для критических операций:**

```java
// Убедиться, что путь на том же устройстве (не символическая ссылка на другую ФС)
FileStore expected = Files.getFileStore(safeDir);
FileStore actual = Files.getFileStore(safeDir.resolve(userFile).normalize());
if (!expected.equals(actual)) {
    throw new SecurityException("Cross-device access denied");
}
```

### 19.2. Как безопасно создавать временные файлы?

Стандартный `Files.createTempFile()` безопасен по расположению, но не гарантирует атомарности в конкурентной среде и требует ручного удаления:

```java
// Лучшая практика: создание + работа + удаление в finally
Path tmpFile = Files.createTempFile("myapp", ".tmp");
try {
    // Работаем с tmpFile
    Files.writeString(tmpFile, sensitiveData);
    processFile(tmpFile);
} finally {
    // Безопасно удаляем (не бросает исключение, если файла уже нет)
    Files.deleteIfExists(tmpFile);

    // Альтернатива: затереть содержимое перед удалением
    // (для конфиденциальных данных)
    try (RandomAccessFile raf = new RandomAccessFile(tmpFile.toFile(), "rws")) {
        byte[] zeros = new byte[(int) raf.length()];
        raf.write(zeros);  // перезаписываем нулями
        raf.getFD().sync();  // синхронизируем
    } catch (IOException e) { /* всё равно удаляем */ }
    Files.deleteIfExists(tmpFile);
}
```

**Создание временного файла с ограниченными правами (POSIX):**

```java
// Только владелец может читать/писать
Set<PosixFilePermission> ownerOnly =
    PosixFilePermissions.fromString("rw-------");
FileAttribute<Set<PosixFilePermission>> attr =
    PosixFilePermissions.asFileAttribute(ownerOnly);

Path secureTmp = Files.createTempFile("secure", ".tmp", attr);
// Теперь другие пользователи не могут прочитать временный файл
```

**DELETE_ON_CLOSE — осторожно:**

```java
// Files.newOutputStream() с DELETE_ON_CLOSE — удалит файл при закрытии
try (OutputStream out = Files.newOutputStream(
        tmpFile, StandardOpenOption.DELETE_ON_CLOSE)) {
    out.write(data);
}  // файл автоматически удалён!
// Но: если JVM упадёт, файл останется на диске
```

### 19.3. Чем опасны символические ссылки и как с ними работать?

Символические ссылки (symlinks) позволяют одному пути указывать на другой файл/директорию, что создаёт риски безопасности:

```java
Path baseDir = Path.of("/safe/uploads").toRealPath();  // канонический путь
Path userPath = baseDir.resolve("../../../etc/passwd");  // атака!

// ❌ Опасный код: проверяем путь, но не проверяем, что это за файл
if (userPath.normalize().startsWith(baseDir)) {
    Files.readString(userPath);  // может прочитать /etc/passwd через symlink!
}

// ✅ Безопасный код: проверяем РЕАЛЬНЫЙ путь (после разрешения symlink'ов)
Path realPath = userPath.toRealPath(LinkOption.NOFOLLOW_LINKS);  // не идём по symlink'ам
// или: Path realPath = userPath.toRealPath();  // разрешаем symlink'и и проверяем
if (!realPath.startsWith(baseDir)) {
    throw new SecurityException("Symlink escape: " + userPath + " → " + realPath);
}
```

**Проверка на символическую ссылку:**

```java
// Проверить, что путь — НЕ символическая ссылка
if (Files.isSymbolicLink(path)) {
    throw new SecurityException("Symbolic links are not allowed: " + path);
}

// Проверить все компоненты пути (каждый сегмент может быть symlink'ом)
Path normalized = path.normalize();
for (Path component : normalized) {
    Path resolved = baseDir.resolve(component);
    if (Files.isSymbolicLink(resolved)) {
        throw new SecurityException("Symlink in path component: " + component);
    }
}
```

**Практические рекомендации:**
1. Всегда вызывайте `.toRealPath()` для финальной проверки
2. Используйте `LinkOption.NOFOLLOW_LINKS` если symlink'и не ожидаются
3. Проверяйте `Files.isSymbolicLink()` для критических путей
4. Помните: защита должна быть на уровне дескриптора (inode/fileKey), а не только пути

### 19.4. Как InterruptibleChannel связан с прерыванием потоков?

`InterruptibleChannel` — интерфейс, который реализуют все каналы NIO. Его ключевая особенность: если поток заблокирован на I/O операции канала и другой поток вызывает `thread.interrupt()`, канал **закрывается** и блокирующая операция выбрасывает `ClosedByInterruptException`:

```java
Thread worker = new Thread(() -> {
    try (SocketChannel channel = SocketChannel.open(
            new InetSocketAddress("server", 8080))) {

        ByteBuffer buf = ByteBuffer.allocate(1024);

        // Блокирующее чтение — поток ждёт данные от сервера
        int read = channel.read(buf);  // ← здесь поток может быть прерван

    } catch (ClosedByInterruptException e) {
        System.out.println("I/O прервано через thread.interrupt()");
        // Канал ЗАКРЫТ автоматически!
    } catch (AsynchronousCloseException e) {
        System.out.println("Канал закрыт другим потоком");
    } catch (IOException e) {
        System.out.println("Другая I/O ошибка: " + e.getMessage());
    }
});

worker.start();
Thread.sleep(1000);
worker.interrupt();  // прерываем I/O операцию
```

**Важно:** После прерывания канал становится непригодным для использования — он **закрыт**. Это отличается от `java.io` потоков, где `interrupt()` не влияет на блокирующие операции (поток просто игнорирует прерывание).

**Разница между закрытием и прерыванием:**

| Действие | Исключение | Канал | Поток |
|---|---|---|---|
| `channel.close()` из другого потока | `AsynchronousCloseException` | Закрыт | Не прерван |
| `thread.interrupt()` на заблокированном I/O | `ClosedByInterruptException` | Закрыт | Прерван (`isInterrupted() == true`) |
| Обычная ошибка I/O | `IOException` | Может быть открыт | Не прерван |

```java
// Корректная обработка в реальном коде:
try (InterruptibleChannel channel = ...) {
    while (!Thread.currentThread().isInterrupted()) {
        // I/O операции
    }
} catch (ClosedByInterruptException e) {
    Thread.currentThread().interrupt();  // восстанавливаем флаг прерывания
    // Выходим — канал уже закрыт
}
```

---

## 20. Производительность и выбор подхода: дерево решений

### 20.1. Сравнение производительности: IO vs NIO vs Async vs Virtual Threads

**Сводная таблица по ключевым метрикам (ориентировочные значения для типичного сервера):**

| Подход | Память на 1 соединение | Макс. соединений | Latency (p50) | Throughput | Сложность кода |
|---|---|---|---|---|---|
| Thread-per-connection (java.io) | ~1 МБ (стек) | ~5 000 | Низкая | Средняя | ★☆☆☆☆ (просто) |
| NIO Selector (1 поток) | ~100 байт | ~100 000+ | Очень низкая | Высокая | ★★★★★ (сложно) |
| NIO Selector (CPU×2 потоков) | ~100 байт | ~500 000+ | Низкая | Очень высокая | ★★★★★ (сложно) |
| Async I/O (AsynchronousChannel) | ~1 КБ | ~100 000+ | Средняя | Средняя | ★★★★☆ (callback'и) |
| Virtual Threads (JDK 21+) | ~200 байт | ~1 000 000+ | Низкая | Высокая | ★☆☆☆☆ (просто!) |
| Virtual Threads + Structured | ~200 байт | ~1 000 000+ | Низкая | Очень высокая | ★★☆☆☆ (почти просто) |

**Конкретные цифры из практики (эхо-сервер, 10K соединений, средний размер сообщения 1 КБ):**

```java
// Условные бенчмарки — для иллюстрации порядка величин:
// Thread-per-connection:        ~2 000 запросов/сек, 5 ГБ памяти, 10% CPU
// NIO Selector:                 ~50 000 запросов/сек, 50 МБ памяти, 25% CPU
// Virtual Threads (JDK 21+):    ~45 000 запросов/сек, 200 МБ памяти, 22% CPU
// Virtual Threads + sync fix:   ~48 000 запросов/сек, 200 МБ памяти, 20% CPU
```

**Ключевые выводы:**
1. **Virtual Threads практически догнали NIO по производительности**, но с простотой синхронного кода
2. **NIO всё ещё выигрывает** в сценариях с экстремальными требованиями (Netty, прокси, message brokers)
3. **Async I/O проигрывает** по throughput из-за overhead'а на callback'и и управление пулом потоков
4. Для 95% бизнес-приложений **Virtual Threads — оптимальный выбор** начиная с JDK 21

### 20.2. Дерево решений: какой I/O-подход выбрать для вашего сценария?

```
Ваша задача связана с I/O?
│
├── ДА → Какой тип I/O?
│   │
│   ├── Файловый I/O
│   │   │
│   │   ├── Небольшие файлы (<10 МБ), прочитать/записать целиком
│   │   │   └── Files.readString() / Files.writeString() (Java 11+)
│   │   │       └── Нужна производительность? → Files.readAllBytes() + ручная обработка
│   │   │
│   │   ├── Большие файлы (>100 МБ), последовательное чтение
│   │   │   ├── Текстовые → Files.lines() или BufferedReader
│   │   │   └── Бинарные → FileInputStream + BufferedInputStream (буфер 64 КБ)
│   │   │
│   │   ├── Большие файлы, произвольный доступ
│   │   │   ├── Простой API → RandomAccessFile
│   │   │   ├── Производительность → FileChannel + MappedByteBuffer
│   │   │   └── JDK 14+ → FileChannel + MappedByteBuffer (освобождение улучшено)
│   │   │
│   │   ├── Копирование файлов
│   │   │   ├── Простое → Files.copy()
│   │   │   ├── Большое копирование → FileChannel.transferTo() (zero-copy)
│   │   │   └── Асинхронное → AsynchronousFileChannel
│   │   │
│   │   └── Мониторинг директории → WatchService
│   │
│   └── Сетевой I/O
│       │
│       ├── JDK 21+ доступен?
│       │   │
│       │   ├── ДА → Virtual Threads + блокирующий I/O
│       │   │   │
│       │   │   ├── Простой сервер (до 100K соединений) → Thread.ofVirtual()
│       │   │   ├── Микросервисы → Spring Boot 3.2+ / Helidon Níma
│       │   │   ├── Параллельные запросы → StructuredTaskScope
│       │   │   └── Есть synchronized? → JDK 24+ (нет pinning)
│       │   │
│       │   └── НЕТ (JDK <21) → NIO Selector
│       │       │
│       │       ├── HTTP API → Netty / Jetty / Undertow
│       │       ├── Прокси / Gateway → Netty (zero-copy, оптимизации)
│       │       ├── Message Broker → NIO Selector + пул потоков
│       │       └── Простой случай → можете использовать Async I/O (AsynchronousSocketChannel)
│       │
│       └── Специфические требования?
│           ├── Жёсткий SLA по latency (99.99% < 1ms) → NIO Selector + off-heap буферы
│           ├── Миллионы долгоживущих соединений → NIO Selector (экономия памяти)
│           └── Прототип / MVP / тесты → Всегда блокирующий I/O (простота!)
│
└── НЕТ → Вам не нужен этот документ :)
```

---

## 21. Эволюция I/O в JDK (7 → 26)

| Версия | Год | Изменения в I/O |
|---|---|---|
| **JDK 1.0** | 1996 | `java.io`: InputStream, OutputStream. File. Socket, ServerSocket |
| **JDK 1.1** | 1997 | Reader/Writer, InputStreamReader/OutputStreamWriter (мост), стандартная сериализация |
| **JDK 1.4** | 2002 | **NIO**: Channel, Buffer, Selector, FileChannel, MappedByteBuffer, Charset |
| **JDK 7** | 2011 | **NIO.2**: Path, Files, WatchService, AsynchronousFileChannel, AsynchronousSocketChannel, FileVisitor |
| **JDK 8** | 2014 | `Files.lines()` — ленивый Stream строк, `Files.list()`, `Files.walk()`, `Files.find()` |
| **JDK 9** | 2017 | `VarHandle` (низкоуровневый доступ к памяти), улучшения десериализации |
| **JDK 11** | 2018 | `Files.readString()`, `Files.writeString()`, `Path.of()` (короче, чем `Paths.get()`) |
| **JDK 12** | 2019 | `Files.mismatch()` — побайтовое сравнение двух файлов |
| **JDK 13** | 2019 | `FileSystems.newFileSystem(Path, …)` — улучшенная работа с ZIP как с ФС, ByteBuffer: `slice()`, `duplicate()` с явным указанием позиции |
| **JDK 14** | 2020 | JEP 352: Non-Volatile Mapped Byte Buffers (NVM), Foreign-Memory Access API (инкубатор) |
| **JDK 15** | 2020 | Текстовые блоки (Text Blocks) — удобнее для I/O с многострочными данными |
| **JDK 16** | 2021 | Records (упрощают DTO для I/O), Unix-Domain Socket Channels (JEP 380) |
| **JDK 17** | 2021 | Sealed Classes (безопасность сериализации), Foreign Function & Memory API (инкубатор) |
| **JDK 18** | 2022 | `InetAddress` resolver improvements, UTF-8 по умолчанию для `Charset` |
| **JDK 19** | 2022 | Virtual Threads (preview), Structured Concurrency (preview), Foreign Function & Memory API (preview) |
| **JDK 20** | 2023 | Virtual Threads (2nd preview), Scoped Values (preview) |
| **JDK 21** | 2023 | **Virtual Threads final** (JEP 444), Structured Concurrency (preview JEP 453), Scoped Values (JEP 446), epoll integration for VT |
| **JDK 22** | 2024 | Foreign Function & Memory API final (JEP 454) — работа с нативной памятью вне кучи, Structured Concurrency (2nd preview) |
| **JDK 23** | 2024 | Улучшения FFM API, улучшения десериализации |
| **JDK 24** | 2025 | **JEP 491**: synchronized больше не pin-ит Virtual Threads; Structured Concurrency final; Scoped Values improvements |
| **JDK 25** | 2025 | Улучшения FFM API для прямого доступа к DMA/I/O устройствам; улучшения Virtual Threads: более глубокая интеграция с io_uring на Linux для файловых операций; Scoped Values — передача контекста без ThreadLocal overhead; улучшения в `AsynchronousFileChannel` для использования io_uring на Linux (экспериментально) |
| **JDK 26** | 2026 (план) | Ожидается: прямая интеграция io_uring для Virtual Threads (JEP draft); Project Valhalla value types — ускорение I/O через reduced pointer indirection; улучшения `FileChannel.map()` с гарантированным освобождением через `MemorySegment`; `MemorySegment` как замена `ByteBuffer` для I/O операций; Structured Concurrency — улучшения для композиции I/O операций |

**Ключевые тренды:**
1. **Упрощение:** от сложного NIO к простому блокирующему коду на Virtual Threads
2. **Безопасность:** усиление фильтрации десериализации, Sealed Classes
3. **Производительность:** Foreign Memory API заменяет `Unsafe` и `DirectByteBuffer` для нативной памяти
4. **Конкурентность:** Virtual Threads + Structured Concurrency делают асинхронный код не нужным для большинства случаев

---

## 22. Практические задачи (код)

### 18.1. Чтение последних N строк большого лог-файла

```java
public static List<String> tail(Path file, int n) throws IOException {
    Deque<String> deque = new ArrayDeque<>(n);
    try (BufferedReader reader = Files.newBufferedReader(file)) {
        String line;
        while ((line = reader.readLine()) != null) {
            if (deque.size() == n) {
                deque.pollFirst();  // удаляем самую старую строку
            }
            deque.offerLast(line);
        }
    }
    return new ArrayList<>(deque);
}

// Использование:
List<String> last100 = tail(Path.of("/var/log/app.log"), 100);
last100.forEach(System.out::println);
```

### 18.2. Многопоточное чтение разных частей файла через RandomAccessFile

```java
public static byte[] parallelRead(Path file, int threads) throws Exception {
    long fileSize = Files.size(file);
    long chunkSize = fileSize / threads;

    ExecutorService executor = Executors.newFixedThreadPool(threads);
    List<Future<byte[]>> futures = new ArrayList<>();

    for (int i = 0; i < threads; i++) {
        long start = i * chunkSize;
        long end = (i == threads - 1) ? fileSize : start + chunkSize;
        futures.add(executor.submit(() -> {
            byte[] chunk = new byte[(int) (end - start)];
            try (RandomAccessFile raf = new RandomAccessFile(file.toFile(), "r")) {
                raf.seek(start);
                raf.readFully(chunk);
            }
            return chunk;
        }));
    }

    // Собираем результаты
    ByteArrayOutputStream result = new ByteArrayOutputStream();
    for (Future<byte[]> future : futures) {
        result.write(future.get());
    }
    executor.shutdown();
    return result.toByteArray();
}
```

### 18.3. Асинхронный логгер на AsynchronousFileChannel

```java
public class AsyncLogger implements AutoCloseable {
    private final AsynchronousFileChannel channel;
    private final ExecutorService executor;
    private long position = 0;

    public AsyncLogger(Path path) throws IOException {
        this.executor = Executors.newSingleThreadExecutor(r -> {
            Thread t = new Thread(r, "async-logger");
            t.setDaemon(true);
            return t;
        });
        this.channel = AsynchronousFileChannel.open(path,
                Set.of(StandardOpenOption.WRITE, StandardOpenOption.CREATE,
                       StandardOpenOption.APPEND), executor);
    }

    public void log(String message) {
        byte[] bytes = (message + "\n").getBytes(StandardCharsets.UTF_8);
        ByteBuffer buf = ByteBuffer.wrap(bytes);
        channel.write(buf, position, null, new CompletionHandler<>() {
            @Override
            public void completed(Integer written, Void att) {
                position += written;
            }
            @Override
            public void failed(Throwable exc, Void att) {
                System.err.println("Log write failed: " + exc.getMessage());
            }
        });
    }

    @Override
    public void close() throws IOException {
        channel.close();
        executor.shutdown();
    }
}

// Использование:
AsyncLogger logger = new AsyncLogger(Path.of("app.log"));
logger.log("Server started");
logger.log("Processing request...");
// ...
logger.close();
```

### 18.4. Поиск строки в большом файле через RandomAccessFile

```java
public static List<Long> search(Path file, String search) throws IOException {
    List<Long> positions = new ArrayList<>();
    byte[] pattern = search.getBytes(StandardCharsets.UTF_8);

    try (RandomAccessFile raf = new RandomAccessFile(file.toFile(), "r")) {
        long fileSize = raf.length();
        byte[] window = new byte[Math.min((int) fileSize, 65536)];  // 64 КБ окно
        long pos = 0;

        while (pos < fileSize) {
            int chunkSize = (int) Math.min(window.length, fileSize - pos);
            raf.seek(pos);
            raf.readFully(window, 0, chunkSize);

            // Поиск в окне (простой алгоритм, для демонстрации)
            for (int i = 0; i <= chunkSize - pattern.length; i++) {
                boolean match = true;
                for (int j = 0; j < pattern.length; j++) {
                    if (window[i + j] != pattern[j]) {
                        match = false;
                        break;
                    }
                }
                if (match) {
                    positions.add(pos + i);
                }
            }
            pos += chunkSize - pattern.length + 1;  // перекрытие для строк, пересекающих границу
        }
    }
    return positions;
}
```

### 18.5. Рекурсивное копирование директории с NIO.2

```java
public static void copyDirectory(Path source, Path target) throws IOException {
    Files.walkFileTree(source, new SimpleFileVisitor<>() {
        @Override
        public FileVisitResult preVisitDirectory(Path dir, BasicFileAttributes attrs)
                throws IOException {
            Path targetDir = target.resolve(source.relativize(dir));
            Files.createDirectories(targetDir);
            return FileVisitResult.CONTINUE;
        }

        @Override
        public FileVisitResult visitFile(Path file, BasicFileAttributes attrs)
                throws IOException {
            Files.copy(file, target.resolve(source.relativize(file)),
                    StandardCopyOption.REPLACE_EXISTING);
            return FileVisitResult.CONTINUE;
        }
    });
}
```

### 18.6. Распаковка ZIP-архива с защитой от Zip Slip

```java
public static void safeUnzip(Path zipPath, Path destDir) throws IOException {
    Path destDirReal = destDir.toRealPath();
    Files.createDirectories(destDirReal);

    try (ZipInputStream zis = new ZipInputStream(
            new BufferedInputStream(Files.newInputStream(zipPath)))) {
        ZipEntry entry;
        while ((entry = zis.getNextEntry()) != null) {
            Path outputPath = destDirReal.resolve(entry.getName()).normalize();

            // Защита от Zip Slip
            if (!outputPath.startsWith(destDirReal)) {
                throw new SecurityException(
                        "Zip Slip attempt: " + entry.getName() + " → " + outputPath);
            }

            if (entry.isDirectory()) {
                Files.createDirectories(outputPath);
            } else {
                Files.createDirectories(outputPath.getParent());
                Files.copy(zis, outputPath, StandardCopyOption.REPLACE_EXISTING);
            }
            zis.closeEntry();
        }
    }
}
```

### 18.7. NIO-сервер с обработкой миллионов соединений на Virtual Threads

```java
public class VirtualThreadEchoServer {
    public static void main(String[] args) throws IOException {
        try (ServerSocket server = new ServerSocket(8080)) {
            System.out.println("Echo сервер на Virtual Threads (порт 8080)");

            while (true) {
                Socket client = server.accept();
                // createPlatformThread — платформенный поток (дорогой)
                // startVirtualThread — виртуальный поток (дешёвый, можно миллионы)
                Thread.ofVirtual().start(() -> {
                    try (client;
                         BufferedReader in = new BufferedReader(
                                 new InputStreamReader(client.getInputStream()));
                         PrintWriter out = new PrintWriter(
                                 client.getOutputStream(), true)) {

                        String line;
                        while ((line = in.readLine()) != null) {
                            out.println("Echo: " + line);
                        }
                    } catch (IOException e) {
                        // Клиент отключился
                    }
                });
            }
        }
    }
}
```

**Почему это масштабируется:**
- Каждый виртуальный поток занимает ~200 байт (вместо ~1 МБ платформенного)
- Когда `in.readLine()` блокируется, виртуальный поток размонтируется с платформенного
- Платформенный поток может обслуживать другой виртуальный поток
- Миллион виртуальных потоков = ~200 МБ памяти против ~1 ТБ для платформенных

### 22.8. Копирование InputStream → OutputStream с прогресс-баром (Java 9+)

```java
public static void copyWithProgress(InputStream in, OutputStream out, long totalBytes)
        throws IOException {
    byte[] buffer = new byte[65536];  // 64 КБ
    long copied = 0;
    int read;
    int lastPercent = -1;

    while ((read = in.read(buffer)) != -1) {
        out.write(buffer, 0, read);
        copied += read;

        int percent = (int) (copied * 100 / totalBytes);
        if (percent != lastPercent) {
            // \r возвращает каретку в начало строки
            System.out.printf("\rПрогресс: [%-50s] %d%%",
                "=".repeat(percent / 2), percent);
            lastPercent = percent;
        }
    }
    System.out.println("\rПрогресс: [==================================================] 100%");
}

// Использование:
Path source = Path.of("large_video.mp4");
long size = Files.size(source);
try (InputStream in = Files.newInputStream(source);
     OutputStream out = Files.newOutputStream(Path.of("copy_video.mp4"))) {
    copyWithProgress(in, out, size);
}
```

### 22.9. Простой парсер CSV с PushbackInputStream

```java
public static List<List<String>> parseCSV(InputStream in) throws IOException {
    List<List<String>> rows = new ArrayList<>();
    PushbackInputStream pbis = new PushbackInputStream(in, 256);
    List<String> currentRow = new ArrayList<>();
    StringBuilder field = new StringBuilder();

    int b;
    while ((b = pbis.read()) != -1) {
        if (b == '"') {
            // Читаем quoted-строку
            while ((b = pbis.read()) != -1) {
                if (b == '"') {
                    int next = pbis.read();
                    if (next == '"') {
                        field.append('"');  // escaped quote
                    } else {
                        if (next != -1) pbis.unread(next);  // не quote — возвращаем
                        break;
                    }
                } else {
                    field.append((char) b);
                }
            }
        } else if (b == ',') {
            currentRow.add(field.toString());
            field.setLength(0);
        } else if (b == '\n') {
            currentRow.add(field.toString());
            rows.add(currentRow);
            currentRow = new ArrayList<>();
            field.setLength(0);
        } else if (b != '\r') {
            field.append((char) b);
        }
    }
    // Последнее поле + строка (если нет завершающего \n)
    if (!field.isEmpty() || !currentRow.isEmpty()) {
        currentRow.add(field.toString());
        if (!currentRow.isEmpty()) rows.add(currentRow);
    }
    return rows;
}

// Использование:
String csv = "\"Smith, John\",42,\"Boston, MA\"\n\"Doe, Jane\",35,\"NYC\"\n";
try (InputStream in = new ByteArrayInputStream(csv.getBytes(StandardCharsets.UTF_8))) {
    List<List<String>> rows = parseCSV(in);
    rows.forEach(System.out::println);
}
// [Smith, John, 42, Boston, MA]
// [Doe, Jane, 35, NYC]
```

### 22.10. Мониторинг свободного места на диске с FileStore

```java
public class DiskMonitor {
    public static void main(String[] args) throws IOException, InterruptedException {
        Path watchPath = Path.of(args.length > 0 ? args[0] : ".");

        System.out.println("Мониторинг свободного места на " + watchPath.toAbsolutePath());
        System.out.printf("%-20s %12s %12s %12s %8s%n",
            "Устройство", "Всего (ГБ)", "Свободно (ГБ)", "Занято (ГБ)", "Заполн.%");
        System.out.println("-".repeat(72));

        while (true) {
            FileStore store = Files.getFileStore(watchPath);
            long total = store.getTotalSpace();
            long free = store.getUsableSpace();
            long used = total - free;
            int percent = (int) (used * 100 / total);

            System.out.printf("\r%-20s %12.1f %12.1f %12.1f %7d%%",
                store.name(),
                total / (1024.0 * 1024 * 1024),
                free / (1024.0 * 1024 * 1024),
                used / (1024.0 * 1024 * 1024),
                percent);

            // Предупреждение при заполнении > 90%
            if (percent > 90) {
                System.err.printf("%n⚠️ ВНИМАНИЕ: диск %s заполнен на %d%%!%n",
                    store.name(), percent);
            }

            Thread.sleep(5000);  // обновление каждые 5 сек
        }
    }

    // Альтернатива: проверка перед записью
    public static boolean hasEnoughSpace(Path path, long requiredBytes) throws IOException {
        long usable = Files.getFileStore(path).getUsableSpace();
        return usable > requiredBytes + 100 * 1024 * 1024;  // +100 МБ запас
    }
}
```

---

> **Примечание:** Этот документ охватывает Java I/O и NIO от основ до JDK 26. Для углублённого изучения рекомендуется практиковаться, писать код и исследовать исходный код JDK, особенно пакеты `sun.nio.ch` (платформенно-зависимые реализации Selector и Channel).
