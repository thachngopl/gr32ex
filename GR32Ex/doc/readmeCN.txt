The GR32 ��չ�����ؼ���. Ver 0.1

Writen by Riceball LEE(riceball@users.sourceforge.net)

����:
 * ͨ�þ��鶯������
 * ͨ�ö�����Ч����
   * ˮ����Ч
   * ͨ��������Ч��������
     * �ǿ�������Ч
     * ��ѩ������Ч
 * ֧�ְ�͸�� GRControl ����ؼ���:
   * �ؼ���͸����:
   * ����ؼ�����ͼ�λ��߿�֧��: ֧����̬��Hot, Down, Normal
   * ��͸���ĸ��ϱ���֧��
       * ǽֽ Wallpaper: ���Ȼ��ƣ�����еĻ���
       * ���� Gradient:  ��λ��ƣ�����еĻ���
       * ��ͼ Texture:   �����ƣ�����еĻ���

��GR_AniGEffetcts��Ԫ�е� TGRAnimationEffects ����Խ��������Ƶ� TCustomControl, TGraphicControl �� TCustomForm�������ڱ�׼GDI�Ŀؼ���ʹ��Repaint��Invalidate���ƣ�������˸��
������Ҳ���Ի��Ƶ� TCustomPaintBox32 �ϣ���Image32�ϻ��Ʋ���������˸��

The GR32 Extension ���ӿؼ����Ŀ�ܹ���:
 * ���е�GR���ӿؼ����Ǵ�TGRCustomControl��TGRGraphicControl)�����ġ� TGRCustomControl����Window �����WinControl��
 * �ؼ���͸����:
 * ��͸���ĸ��ϱ���֧��
 * �߼�����֧��
   * ��ͼ����
   * ��������
   * ������Ӱ
   * �����
   * ��͸��
 * �������ø����ࣺ
   * TCustomGraphicProperty(GR32_GraphUtils): you can add the perfect properties to your components too.
    * GR32_Graphics Properties:
     * TGradient ����������: (original writen by Kambiz R. Khojasteh(kambiz@delphiarea.com))
       It is an extremely fast gradient fill control with 
       a large set of styles. As built-in, TGradient can 
       draw gradient in 23 styles and provides an easily 
       method to define custom styles. In addition, this 
       control can shift and/or rotate the gradient colors, 
       which could be used for creating animated gradients.
       * AlphaBegin (new by riceball)
       * AlphaEnd (new by riceball)
       * AlphaChannel: Boolean. whether treat the gradient as a alpha channel graph. (new by riceball)
     * TWallpaper ǽֽ������
       * Style: wlpsCenter, wlpsTile, wlpsStretch
       * Alpha: the alpha blending value.
       * FileName: the wallpaper picture filename
       * Picture: TPicture
     * TBackground ����������: you can build very complex composed background here. 
        it include a wallpaper property, a texture and a Gradient property, they are alpha blending after you proper set.
       * Wallpaper: the first draw(if any)
       * Gradient: the second draw(if any)
       * Texture: the last draw(if any). Texture is also a wallpaper property.
       * Buffered: whether cache the result.
     * TFont32 �߼�����������: it supports Outline font, textured font or 3D Font with shadow. of cause it supports the antialiasing and transparency.
       * ��ӰЧ�� Shadow: TShadowEffect: the font shadow
       * ��������� Quality: TFontQuality: antialiasing quality.
       * ���� Outline: Boolean: whether the text is outline only.
       * ͸����Opacity: Byte: the alpha blending value.
       * �м�� LineSpacing: integer: Specifies the spacing between Lines.
       * �ַ���� CharSpacing: integer: Specifies the spacing between characters. <Note: Not used yet>
       * ����ͼ Background: TBackground: The Font background Texture if any.
       * fucntion TextExtent and TextExtentW
       * fucntion RenderText and RenderTextW
       * function DrawText: simulate the winapi. the following aFormat Options are supported: 
           DT_CALCRECT, DT_TOP, DT_VCENTER, DT_BOTTOM, DT_LEFT, DT_CENTER, DT_RIGHT, DT_WORDBREAK, DT_NOPREFIX, DT_EXPANDTABS
   * TCustomEffectProperty
     * TShadowEffect
       * Opacity: Byte: the alpha blending value.
       * OffsetX: Integer: the shadow X offset
       * OffsetY: Integer: the shadow Y offset
       * Enabled: Bool
       * Color: TColor
       * Blur: Byte: the shadow blur.
   * TBitmap32Ex: derived from TBitmap32, use the Font32.
 * GR32_FilterEx: provide many 3X3 , 5X5 and 7x7 filters and add new standard filters easy and other useful proc.
   * ApplyTransparentColor: set the specified color as Transparent.
   * ApplyBlueChannelToAlpha: set the BlueChannel value as alpha channel value.
   * ApplyBWImage: covnert a color image to two-color(black, white) image.
   * ...

the TGRCustomControl and TGRGraphicControl Ver 0.1 Buffer Mechanism:

1. All things paint to FBuffer (include the parent background if need) 
   repaint the FBuffer when the FBufferDirty is true.
  related methods: PaintBuffer, PaintParentBackground
2. paint itself to the FSelfBuffer if FSelfBufferDirty is true:
  PaintSelfToBuffer:
  PaintSelfTo(aBuffer): if FSelfBuffer not dirty then paint the FSelfBuffer to aBuffer

How to set the transparent to the GRControls:
 1. GRControl.Transparent := true;
 2. GRControl.Color := clNone;


�ر��л:
  GR32 Team(http://sourceforge.net/projects/graphics32) for their great GR32 Pack. No Them No this!
  Roman Gudchenko(c)  mailto:roma@goodok.ru for the G32_Interface.pas
  sharman1@uswest.net for the G32_WConvolution.pas
  Kambiz R. Khojasteh(kambiz@delphiarea.com) for his gradient component.
  Jens Weiermann <wexmanAT@solidsoftwareDOT.de>
  Vladimir Vasilyev <Vladimir@tometric.ru>
  Patrick
  �ܾ��� (zjy@cnpack.org)
  Troels Jakobsen - delphiuser@get2net.dk
  Others I missed.


Note: 
No Register function and Component Icon!
I have to hack into GR32.pas to support my TFont32.
hack into GR32_layers to support the MouseInControl , focused layer and keyboard event.

you can apply the patch: gr32v183patch.txt(put Updater.exe and gr32v183Patch.upd to the graphics32 dir and run update.exe)

here are my changes in GR32.pas:

type
  TFontClass = Class of TFont; //added by riceball

  TBitmap32 = class(TCustomMap)
   ...
  protected
    ....
    procedure SetPixelFS(X, Y: Single; Value: TColor32);
    procedure SetPixelXS(X, Y: TFixed; Value: TColor32);

  public
    constructor Create; override;
    destructor Destroy; override;

    class function CreateFont: TFont; virtual; //added by riceball
    ...
  end;

constructor TBitmap32.Create;
begin
  ...
  //FFont := TFont.Create;
  FFont := CreateFont; //modified by riceball
  FFont.OnChange := FontChanged;
  ...
end;

//added by riceball
class function TBitmap32.CreateFont(): TFont;
begin
  Result := TFont.Create;
end;
