原文链接：[http://www.tutorialspoint.com/design_pattern/adapter_pattern.htm](http://www.tutorialspoint.com/design_pattern/adapter_pattern.htm)
适配器模式是在两个不兼容的或者是无关的接口之间充当一个桥梁。这种设计模式结合两个无关接口的功能于一体，属于结构型模式的一种。

这种设计模式需要一个单独的类，这个单独的类负责结合那些独立的或者是不兼容的接口的所有功能。现实生活中也有这样的例子，读卡器在存储卡和笔记本电脑之间充当了一个适配器的角色。用户先把存储卡插入到读卡器中，再把读卡器插入到笔记本电脑中，这样一来笔记本电脑就可以在存储卡中读写数据。

下面我们演示一个适配器模式的例子：一个音乐播放器只能播放 mp3 文件，我们想要改装这个音乐播放器，改装后的音乐播放器可以播放 mp3 、vlc 、mp4 文件。

### 实现
我们有一个 MediaPlayer 接口和一个 AudioPlayer 类，其中 AudioPlayer 类实现了 MediaPlayer 接口。默认情况下 AudioPlayer 只能播放 mp3 格式的文件。

我们还有另外一个接口 AdvancedMediaPlayer 和该接口的实现类。这些实现类可以播放 vlc 和 mp4 格式的文件。
 
我们想让 AudioPlayer 也能播放其他格式的文件。为了达到这种功能，我们创建了一个适配器类 MediaAdapter ，MediaAdapter 实现了 MediaPlayer 接口并且使用了 AdvancedMediaPlayer 对象来播放其他格式的文件。

AudioPlayer 有一个适配器 MediaAdapter，AudioPlayer 把用户想要播放的文件格式和文件位置传递给 MediaAdapter ，AudioPlayer 根本就不知道到底是哪个类在播放这种格式的文件，它把这个播放功能委托给了 MediaAdapter ，不用去关注 MediaAdapter 是怎么实现这个功能的。
AdapterPatternDemo 是我们的演示类，AdapterPatternDemo 会用 AudioPlayer 类来播放各种格式的文件。
 
### 第一步
 
创建媒体播放类和高级媒体播放类。

MediaPlayer.java

    public interface MediaPlayer {
        public void play(String audioType, String fileName);
    }
    
AdvancedMediaPlayer.java
    
    public interface AdvancedMediaPlayer {
        public void playVlc(String fileName);
        public void playMp4(String fileName);
    }
    
### 第二步
创建 AdvancedMediaPlayer 类的具体实现类。

VlcPlayer.java

    public class VlcPlayer implements AdvancedMediaPlayer {
        @Override
        public void playVlc(String fileName) {
            System.out.println("Playing vlc file. Name:" + fileName);
        }
        @Override
        public void playMp4(String fileName) {
            // 什么也不错
        }
    }

Mp4Player.java
    
    public class Mp4Player implements AdvancedMediaPlayer {
        @Override
        public void playVlc(String fileName) {
            // 什么也不错
        }
        @Override
        public void playMp4(String fileName) {
            System.out.println("Playing mp4 file. Name:" + fileName);
        }
    
    }
    
### 第三步
创建实现了 MediaPlayer 接口的适配器类。

MediaAdapter.java
    
    public class MediaAdapter implements MediaPlayer {
        AdvancedMediaPlayer advancedMusicPlayer;
        
        public MediaAdapter(String audioType) {
            if (audioType.equalsIgnoreCase("vlc")) {
                advancedMusicPlayer = new VlcPlayer();
            } else if (audioType.equals("mp4")) {
                advancedMusicPlayer = new Mp4Player();
            }
        }
        
        @Override
        public void play(String audioType, String fileName) {
            if (audioType.equalsIgnoreCase("vlc")) {
                advancedMusicPlayer.playVlc(fileName);
            } else if (audioType.equalsIgnoreCase("mp4")) {
                advancedMusicPlayer.playMp4(fileName);
            }
        }
    
    }
    
### 第四步
创建一个实现了 MediaPlayer 接口的具体实现类。

AudioPlayer.java

    public class AudioPlayer implements MediaPlayer {
        MediaAdapter mediaAdapter;
        
        @Override
        public void play(String audioType, String fileName) {
            // 原本就支持播放 mp3
            if (audioType.equalsIgnoreCase("mp3")) {
                System.out.println("Playing mp3 file. Name:" + fileName);
            } else if (audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
                // mediaAdapter 支持播放其他格式的文件
                mediaAdapter = new MediaAdapter(audioType);
                mediaAdapter.play(audioType, fileName);
            } else {
                System.out.println("Invalid media. " + audioType + " format not supported");
            }
        }
    }
    
### 第五步
使用 AudioPlayer 播放不同格式的音频文件。
    
AdapterPatternDemo.java
    
    public class AdapterPatternDemo {
        public static void main(String[] args) {
            AudioPlayer audioPlayer = new AudioPlayer();
            
            audioPlayer.play("mp3", "beyond the horizen.mp3");
            audioPlayer.play("mp4", "alone.mp4");
            audioPlayer.play("vlc", "far far away.vlc");
            audioPlayer.play("avi", "mind me.avi");
        }
    }
### 第六步
验证输出结果。
    
    Playing mp3 file. Name: beyond the horizon.mp3
    Playing mp4 file. Name: alone.mp4
    Playing vlc file. Name: far far away.vlc
    Invalid media. avi format not supported

  