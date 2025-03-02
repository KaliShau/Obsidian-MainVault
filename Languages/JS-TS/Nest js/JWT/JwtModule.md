
___
```TS
JwtModule.registerAsync({
	imports: [ConfigModule],
	inject: [ConfigService],
	useFactory: JwtConfig,
})
```