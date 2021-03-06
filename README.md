# Msgpack for Delphi

It's like JSON but small and fast.

```
unit Owner: D10.Mofen, qdac.swish
contact:
       qq:185511468, 
    email:185511468@qq.com
welcome to report bug
```

Works with
--------
* Delphi 7 (tested)
* Delphi 2007 (tested)
* XE5, XE6, XE7, FMX (tested)

changes:
--------
   * fixed int32, int64 parse bug< integer, int64 parse zero>
     2014-11-09 22:35:27
     
   + add EncodeToFile/DecodeFromFile
     2014-11-13 12:30:58

   * fix  asVariant = null (thanks for cyw(26890954))
     2014-11-14 09:05:52
     
   * fix AsInteger = -1 bug (thanks for cyw(26890954))
     2014-11-14 12:15:52

   * fix AsInteger = -127 bug
     check int64/integer/cardinal/word/shortint/smallint/byte assign, encode,decode, read
     2014-11-14 12:30:38

  
### Code Example
```Pascal

var
  lvMsg, lvMsg2:TSimpleMsgPack;
  lvBytes:TBytes;
  s:string;
begin
  lvMsg := TSimpleMsgPack.Create;
  lvMsg.S['key.obj'] := '汉字,ascii';
  if dlgOpen.Execute then
  begin
    lvMsg.S['key.image.name'] := ExtractFileName(dlgOpen.FileName);
    
    // file binary data
    lvMsg.ForcePathObject('key.image.data').LoadBinaryFromFile(dlgOpen.FileName);
  end;
  
  //
  lvBytes := lvMsg.EncodeToBytes;

  lvMsg2 := TSimpleMsgPack.Create;
  lvMsg2.DecodeFromBytes(lvBytes);
  //
  Memo1.Lines.Add(lvMsg2.S['key.obj']);
  if lvMsg2.S['key.image.name'] <> '' then
  begin
    s := ExtractFilePath(ParamStr(0)) + lvMsg2.S['key.image.name'];
    Memo1.Lines.Add('file saved');
    Memo1.Lines.Add(s);
    lvMsg2.ForcePathObject('key.image.data').SaveBinaryToFile(s);    
  end;
  
  ```
