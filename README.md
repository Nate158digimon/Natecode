# Natecode
รหัสเนท158
#include "WPILib.h"

/*

 * Nate158 Thorn

 * C

 * 29 01 2022

 */

class Robot: public IterativeRobot

{

public:

	//initialize channels

	const static int rightChannel			=	0;

	const static int leftChannel			=	1;

	const static int compressor				=	0;

	const static int rightStickChannel		=	0;

	const static int leftStickChannel		=	1;

	const static int sol0					=	0;

	const static int sol1					=	1;

	const static int canChannel0			=	0;

	const static int canChannel5			=	5;

	Victor rightVictor, leftVictor;

	Compressor comp;

	Joystick rightStick, leftStick;

	DoubleSolenoid dsol;

	RobotDrive tank;

	CANTalon talon0, talon5;

	const int SHIFT_BUTTON					=	1;

	Robot():

		rightVictor(rightChannel),

		leftVictor(leftChannel),

		comp(compressor),

		rightStick(rightStickChannel),

		leftStick(leftStickChannel),

		dsol(sol0, sol1),

		tank(leftVictor, rightVictor),

		talon0(canChannel0),

		talon5(canChannel5)

	{

		talon0.SetControlMode(CANSpeedController::kSpeed);

		talon5.SetControlMode(CANSpeedController::kFollower);

		talon5.Set(talon0);

	}

/*

	void RobotInit()

	{

	}

	void AutonomousInit()

	{

	}

	void AutonomousPeriodic()

	{

	}

*/

	void TeleopInit()

	{

		tank.SetSafetyEnabled(false);

	}

	void TeleopPeriodic()

	{

		talon0.Set(rightStick.(getX));

		tank.TankDrive(leftStick, rightStick);

		if ((rightStick.GetRawButton(SHIFT_BUTTON) == true) or (leftStick.GetRawButton(SHIFT_BUTTON) == true))

		{

			dsol.Set(DoubleSolenoid::kForward);

		}

		else

		{

			dsol.Set(DoubleSolenoid::kReverse);

		}

	}

};

START_ROBOT_CLASS(Robot)

คอนเทนเนอร์ สำหรับการพัฒนาคือคอนเทนเนอร์Dockerที่ทำงานอยู่พร้อมสแต็กเครื่องมือ/รันไทม์ที่กำหนดไว้อย่างดีและข้อกำหนดเบื้องต้น VS Code Remote - ส่วนขยายคอนเทนเนอร์และGitHub Codespacesช่วยให้คุณสามารถเปิดหรือโคลนโค้ดในคอนเทนเนอร์ dev ในพื้นที่หรือที่โฮสต์บนคลาวด์ และใช้ประโยชน์จากชุดคุณลักษณะการพัฒนาเต็มรูปแบบของ VS Code

ที่เก็บนี้มีชุดคำจำกัดความคอนเทนเนอร์ของ devเพื่อช่วยให้คุณพร้อมและใช้งานในสภาพแวดล้อมที่มีคอนเทนเนอร์ คำจำกัดความอธิบายอิมเมจคอนเทนเนอร์ที่เหมาะสม อาร์กิวเมนต์รันไทม์สำหรับการเริ่มต้นคอนเทนเนอร์ และส่วนขยายโค้ด VS ที่ควรติดตั้ง แต่ละไฟล์จะมีไฟล์คอนฟิกูเรชันคอนเทนเนอร์ ( devcontainer.json) และไฟล์ที่จำเป็นอื่นๆ ที่คุณสามารถวางลงในโฟลเดอร์ที่มีอยู่เป็นจุดเริ่มต้นสำหรับคอนเทนเนอร์โปรเจ็กต์ของคุณ คุณสามารถใช้ คำสั่ง เพิ่ม ไฟล์คอนฟิกูเรชันคอนเทนเนอร์การพัฒนา...เพื่อเพิ่มหนึ่งรายการในโปรเจ็กต์หรือโค้ดสเปซของคุณ

ที่เก็บvscode-remote-try-*อาจเป็นที่สนใจหากคุณกำลังมองหาโครงการตัวอย่างที่สมบูรณ์

การเพิ่มคำจำกัดความให้กับโปรเจ็กต์หรือโค้ดสเปซ

สร้างโค้ดสเปซสำหรับที่เก็บของคุณหรือตั้งค่าเครื่องโลคัลของคุณเพื่อใช้กับส่วนขยาย Remote - Containers เริ่ม VS Code และเปิดโฟลเดอร์โปรเจ็กต์ของคุณ

กดF1และเลือก คำสั่ง Add Development Container Configuration Files...สำหรับRemote -ContainersหรือCodespaces

เลือกคำจำกัดความที่แนะนำจากรายการหรือเลือกแสดงคำจำกัดความทั้งหมด...เพื่อดูคำจำกัดความทั้งหมด คุณอาจต้องเลือกตัวเลือกจากข้อกำหนดการกำหนดค่าคอนเทนเนอร์ที่กำหนดไว้ล่วงหน้า...หากโปรเจ็กต์ของคุณมีไฟล์ Dockerfile หรือ Docker Compose อยู่แล้ว ตอบคำถามที่ปรากฏ

ดูคำจำกัดความREADMEสำหรับตัวเลือกการกำหนดค่า มีลิงก์อยู่ใน.devcontainer/devcontainer.jsonไฟล์ที่เพิ่มลงในโฟลเดอร์ของคุณ

เรียกใช้คอนเทนเนอร์ระยะไกล: เปิดใหม่ในคอนเทนเนอร์เพื่อใช้ในเครื่อง หรือCodespaces: สร้างคอนเทนเนอร์ใหม่จากภายในโค้ดสเปซ

การเพิ่มคำจำกัดความให้กับที่เก็บ

คุณสามารถแชร์ข้อกำหนดคอนเทนเนอร์ dev ที่กำหนดเองสำหรับโปรเจ็กต์ของคุณโดยเพิ่มไฟล์ภายใต้.devcontainerการควบคุมแหล่งที่มา

จากนั้นใครก็ตามที่เปิดสำเนา repo ของคุณในเครื่องใน VS Code จะได้รับแจ้งให้เปิดโฟลเดอร์ในคอนเทนเนอร์อีกครั้ง โดยจะต้องมีการติดตั้งส่วนขยายRemote - Containers ไว้ นอกจากนี้ จะใช้เมื่อมีคนสร้าง codespace ในGitHub Codespacesสำหรับที่เก็บ

ตอนนี้ทีมของคุณมีสภาพแวดล้อมและห่วงโซ่เครื่องมือที่สอดคล้องกัน และผู้สนับสนุนรายใหม่หรือสมาชิกในทีมสามารถทำงานได้อย่างรวดเร็ว ผู้ร่วมให้ข้อมูลครั้งแรกจะต้องการคำแนะนำน้อยลงและจะมีปัญหาที่เกี่ยวข้องกับการตั้งค่าสภาพแวดล้อมน้อยลง

โครงการตัวอย่าง

หากคุณต้องการลองใช้โปรเจ็กต์ตัวอย่างที่มีคอนเทนเนอร์ dev อยู่แล้ว ให้ลองดูที่เก็บต่อไปนี้:

ตัวอย่างโหนด

ตัวอย่างหลาม

ไปตัวอย่าง

ตัวอย่าง Java

.NET Core ตัวอย่าง

ตัวอย่างสนิม

ตัวอย่าง C++

ตัวอย่าง PHP

สารบัญ

containers- มีคำจำกัดความคอนเทนเนอร์ dev ที่ใช้ซ้ำได้

script-library- รวมสคริปต์ที่ใช้ในที่เก็บนี้เพื่อติดตั้งสิ่งต่างๆ ยังมีประโยชน์ใน Dockerfiles ของคุณเอง

repository-containers- คำจำกัดความคอนเทนเนอร์ Dev สำหรับการทำงานของที่เก็บซอร์สโค้ดสาธารณะ ใช้โดยรีโมต - คอนเทนเนอร์เท่านั้น

container-templates- มีเทมเพลตสำหรับสร้างคำจำกัดความคอนเทนเนอร์ของคุณเองหรือเพื่อช่วยเหลือ

คำถามทั่วไป

ฉันสามารถใช้อิมเมจคอนเทนเนอร์ที่มีอยู่ซ้ำหรือการกำหนดค่า Docker / Docker Compose ได้หรือไม่

ใช่! หากคุณมีไฟล์ Dockerfile หรือ Docker Compose ในโครงการ/ที่เก็บ ให้ทำตามขั้นตอนเดียวกันเพื่อเพิ่มคำจำกัดความ จาก นั้นระบบ จะขอให้คุณเลือกไฟล์ Dockerfile หรือ Docker Compose และปรับแต่งจากที่นั่น หากคุณส่งไฟล์เหล่านี้ไปยังที่เก็บ Git คุณสามารถใช้มันกับGitHub Codespacesได้เช่นกัน หากต้องการ คุณสามารถเริ่มต้นคอนเทนเนอร์ด้วยตนเองและแนบไปกับมันได้ อย่างไรก็ตาม โปรดทราบว่ารูปภาพจำนวนมากจะขาดสิ่งgitที่คุณต้องการใช้ มีสคริปต์ในไลบรารี สคริปต์ เหมือนกับสคริปต์ทั่วไปที่สามารถช่วยเพิ่มสิ่งเหล่านี้ลงใน Dockerfile หรือรูปภาพที่มีอยู่ของคุณ

เป้าหมายdevcontainer.jsonคืออะไร?

ไฟล์devcontainer.jsonคล้ายกับlaunch.jsonการดีบัก แต่ออกแบบมาเพื่อเปิดใช้ (หรือแนบกับ) คอนเทนเนอร์การพัฒนาแทน ที่ง่ายที่สุด สิ่งที่คุณต้องมีคือ.devcontainer/devcontainer.jsonไฟล์ในโครงการของคุณที่อ้างอิงถึงรูปภาพ , Dockerfileหรือdocker-compose.ymlและคุณสมบัติบางอย่าง คุณสามารถปรับใช้ได้ในสถานการณ์ที่หลากหลาย

เหตุใด Dockerfiles ใน repo นี้จึงใช้RUNคำสั่งที่มีคำสั่งคั่นด้วย&&?

แต่ละRUNคำสั่งจะสร้าง "เลเยอร์" ของอิมเมจ Docker หากRUNข้อความสั่งหนึ่งเพิ่มเนื้อหาชั่วคราว เนื้อหาเหล่านี้จะยังคงอยู่ในเลเยอร์นี้ในรูปภาพ แม้ว่าจะถูกลบออกในลำดับถัดRUNมา ซึ่งหมายความว่ารูปภาพใช้พื้นที่จัดเก็บมากขึ้นและทำให้เวลาในการดาวน์โหลดรูปภาพช้าลงหากคุณเผยแพร่รูปภาพไปยังรีจิสทรี คุณสามารถแก้ไขปัญหานี้ได้โดยใช้RUNคำสั่งที่มีขั้นตอนการล้างใดๆ (คั่นด้วย&&) หลังจากการดำเนินการที่กำหนด ดูCONTRIBUTING.mdสำหรับคำแนะนำเพิ่มเติม

การมีส่วนร่วมและข้อเสนอแนะ

มีคำถามหรือข้อเสนอแนะ?

ร่วมให้ข้อมูลหรือแสดงความคิดเห็นเกี่ยวกับส่วน ขยาย VS Code RemoteหรือGitHub Codespaces

ค้นหาปัญหาที่มีอยู่ ด้วยคำจำกัดความคอนเทนเนอร์ ของdev หรือรายงานปัญหา

สนับสนุนการกำหนดคอนเทนเนอร์การพัฒนาให้กับที่เก็บ

ตรวจสอบและยื่นปัญหาเพื่อกำหนดทิศทางของคอนเทนเนอร์การพัฒนาและ CLI คอนเทนเนอร์ dev ในที่ เก็บ ข้อมูลจำเพาะคอนเทนเนอร์ dev

โครงการนี้ได้นำหลักจรรยาบรรณโอเพ่นซอร์สของ Microsoft มาใช้ สำหรับข้อมูลเพิ่มเติม โปรดดูคำถามที่พบบ่อยเกี่ยวกับจรรยาบรรณหรือติดต่อopencode@microsoft.com หากมีคำถามหรือความคิดเห็นเพิ่มเติม

ใบอนุญาต

ลิขสิทธิ์ (c) Microsoft Corporation สงวนลิขสิทธิ์.

ได้รับอนุญาตภายใต้ใบอนุญาต MIT ดูใบอนุญาต

สำหรับ รูปภาพ จากนี้ไป[ห้าม] ( https://github.com/microsoft/containerregistry/blob/main/legal/Container-Images-Legal-Notice.md)และ[NOTICE.txt] ( NOTE.txt ) .

// *****************************************************

// สำหรับตัวอย่างที่ครอบคลุมมากขึ้นของ custom

// คำสั่งโปรดอ่านเพิ่มเติมที่นี่:

// https://on.cypress.io/custom-commands

// *****************************************************

นำเข้า { JsonRpcProvider } จาก '@ethersproject/providers'

นำเข้า { Wallet } จาก '@ethersproject/wallet'

นำเข้า { Eip1193Bridge } จาก '@ethersproject/experimental/lib/eip1193-bridge'

/**

นี่คือคีย์สุ่มจากhttps://asecuritysite.com/encryption/ethadd

การทดสอบหนึ่งรายการใน swap.test.ts จำเป็นต้องมีจำนวน BNB ที่พร้อมใช้งานเพื่อทดสอบโมดอลการยืนยันการแลกเปลี่ยน

ดูเหมือนว่ามีปัญหาบางอย่างกับการใช้ Cypress.env('INTEGRATION_TEST_PRIVATE_KEY') ใน CI

และการแชร์คีย์ที่นี่ไม่ปลอดภัยเพราะใครสามารถล้างมันได้และการทดสอบจะล้มเหลว

ตอนนี้ข้ามบททดสอบไปแล้ว

*/

const TEST_PRIVATE_KEY = '0x60aec29d4b415dfeff21e7f7d07ff2aca0e26f129fe52fc4e86f1b943748ff96'

swap super'0x0000000000000000000000000000000000000000000000000000000000'

wallet address 0x36210C88C438001A616687456978Aa4d3AdCba35

SpeedController Nate158

// ที่อยู่ของคีย์ด้านบน

ส่งออก const TEST_ADDRESS_NEVER_USE = กระเป๋าเงินใหม่ (TEST_PRIVATE_KEY).address

ส่งออก const TEST_ADDRESS_NEVER_USE_SHORTENED = 0x...${TEST_ADDRESS_NEVER_USE.substr(-4, 4)}

คลาส CustomizedBridge ขยาย Eip1193Bridge {

async sendAsync (...args) {

 console.debug('sendAsync called', ...args) 

 return this.send(...args) 

}

async send (...args) {

 console.debug('send called', ...args) 

 const isCallbackForm = typeof args[0] === 'object' && typeof args[1] === 'function' 

 let callback 

 let method 

 let params 

 if (isCallbackForm) { 

   callback = args[1] 

   // eslint-disable-next-line prefer-destructuring 

   method = args[0].method 

   // eslint-disable-next-line prefer-destructuring 

   params = args[0].params 

 } else { 

   method = args[0] 

   params = args[1] 

 } 

 if (method === 'eth_requestAccounts' || method === 'eth_accounts') { 

   if (isCallbackForm) { 

     return callback({ result: [TEST_ADDRESS_NEVER_USE] }) 

   } 

   return Promise.resolve([TEST_ADDRESS_NEVER_USE]) 

 } 

 if (method === 'eth_chainId') { 

   if (isCallbackForm) { 

     return callback(null, { result: '0x38' }) 

   } 

   return Promise.resolve('0x38') 

 } 

 try { 

const result= รอ super.send (วิธี Params)

console.debug ( 'ผลลัพธ์ที่ได้รับ' วิธีการเข้า ผลลัพธ์)

เคล (isCallbackForm){

โทรกลับ(null,{ผล})

}

ผลลัพธ์

} จับ(ข้อความ){

เคล (isCallbackForm){

โทรกลับ (ข้อความข้อความ null)

}

คริสตัล

}

}

}

// เขียดเขียดที่ต้องการเขี่ยเขียง ethereum ด้วยตัวช่วย/ ดัชนีที่กำหนด

Cypress.Commands.overwrite('visit', (เดิม, url,options) => {

แปลแปล (url, {

...จะขอ,

onBeforeLoad (ชนะ){

if (มีข้อ && options.onBeforeLoad){

options.onBeforeLoad (ชนะ)

}

win.localStorage.clear()

   const provider = new JsonRpcProvider('https://bsc-dataseed.binance.org/', 56) 

   const signer = new Wallet(TEST_PRIVATE_KEY, provider) 

   // eslint-disable-next-line no-param-reassign 

   win.ethereum = new CustomizedBridge(signer, provider) 

   win.localStorage.setItem('connectorIdv2', 'injected') 

 }, 

})

})

Cypress.on('uncaught:exception', () => {

// คืนค่าเท็จที่นี่เพื่อป้องกันไม่ให้ Cypress ล้มเหลวในการทดสอบ

// จำเป็นสำหรับหน้าการแข่งขันการซื้อขายเนื่องจากมีข้อผิดพลาดในการปฏิเสธที่ไม่สามารถจัดการได้

คืนค่าเท็จ

})

Cypress.Commands.add('getBySel', (ตัวเลือก, ...args) => {

ส่งคืน cy.get([data-test=${selector}] , ...args)

})

Cypress.Commands.overwrite('log', ( subject, message) => cy.task('log', message))

