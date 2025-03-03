
___
```TS
import { Injectable } from '@nestjs/common'
import { ConfigService } from '@nestjs/config'
import { PassportStrategy } from '@nestjs/passport'
import { ExtractJwt, Strategy } from 'passport-jwt'
import { UsersService } from 'src/users/users.service'

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
	constructor(
		private userService: UsersService,
		private config: ConfigService
	) {
	super({
		jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
		secretOrKey: config.get('JWT_SECRET'),
		})
	}
	
	async validate({ id }: {id: string}) {
		return this.userService.getUserById(id)
	}
}
```