export class App {

	control: HTMLDivElement;

	constructor() {
		this.control = document.createElement('div');
		this.control.style.cssText = 'position: abolute; top:0; left: 0; z-index: 1000; display: flex';
		document.body.appendChild(this.control);

		// let input = document.createElement('input');
		// // input.style.cssText = 'flex: 1';
		// let button = document.createElement('button');
		// button.innerText = '確認密碼';
		// button.addEventListener('click', () => {
		// 	if (input.value == 'cpu871') {
		this.passDo();
		// this.control.removeChild(input);
		// this.control.removeChild(button);
		// 	}
		// });
		// this.control.appendChild(input);
		// this.control.appendChild(button);
	}

	private passDo() {
		// let img = document.createElement("img");
		// img.src = "https://code.gamelet.com/gassets/resource/0c1883b7c1edc7bb821942d19d09d587/QmSMV96.gif";

		// this.control.appendChild(img);



		let getMorning = document.createElement('button');
		getMorning.innerText = '查看晨間未記錄體溫';
		getMorning.addEventListener('click', () => {
			this.getMorning();
		});

		let getEvening = document.createElement('button');
		getEvening.innerText = '查看晚間未記錄體溫';
		getEvening.addEventListener('click', () => {
			this.getEvening();
		});

		this.control.appendChild(getMorning);
		this.control.appendChild(getEvening);
	}

	private getMorning() {
		CG.Base.showCGPreloader();
		let morningUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQtdFfxwbfIJHSnzEiBaUDP_QMC8f2h-d6OQhBgy8_ga8HLgdaKzoei4p52sibx2TKfy1JDivJKEScD/pubhtml?gid=286307462&single=true'
		window.fetch(morningUrl).then(result => {
			return result.text();
		}).then(text => {
			try {
				let blackList = [];
				let blackString = '';
				let startIndex = text.indexOf('286307462R1')
				let start = text.slice(startIndex);
				start = start.split('</tbody>')[0];
				// console.log(start)
				let people = start.split('286307462');
				people.map((person, index) => {
					if (index && !person.match('自治') && !person.match('外派') && !person.match('實總')) {
						let details = person.split('<td class="s0">');
						let date = details[1].split('</td>')[0];
						let studentID = details[2].split('</td>')[0];
						let studentIDSim = studentID && studentID.split('871')[1];
						if (!date && studentIDSim) {
							// console.log(studentID);
							blackList.push(studentIDSim);
						}
					}

				})
				blackList.sort();
				blackList.map(black => {
					blackString += String(black) + '、';
				})
				blackString = blackString.slice(0, -1);
				this.render(this.getTitle(1) + blackString + '\n\n未記錄體溫總人數：' + blackList.length);
				CG.Base.hideCGPreloader();
			}
			catch (err) {
				console.log(err)
				this.render('錯誤' + err);
			}

		})
	}

	private getEvening() {
		CG.Base.showCGPreloader();
		let eveningUrl = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQtdFfxwbfIJHSnzEiBaUDP_QMC8f2h-d6OQhBgy8_ga8HLgdaKzoei4p52sibx2TKfy1JDivJKEScD/pubhtml?gid=686859449&single=true'
		window.fetch(eveningUrl).then(result => {
			return result.text();
		}).then(text => {
			try {
				let blackList = [];
				let blackString = '';
				let startIndex = text.indexOf('686859449R1')
				let start = text.slice(startIndex);
				start = start.split('</tbody>')[0];
				let people = start.split('686859449');
				people.map((person, index) => {
					if (index && !person.match('自治') && !person.match('外派') && !person.match('實總')) {
						let details = person.split('<td class="s0">');
						let date = details[1].split('</td>')[0];
						let studentID = details[2].split('</td>')[0];
						let studentIDSim = studentID && studentID.split('871')[1];
						if (!date && studentIDSim) {
							// console.log(studentID);
							blackList.push(studentIDSim);
						}
					}

				})
				blackList.sort();
				blackList.map(black => {
					blackString += String(black) + '、';
				})
				blackString = blackString.slice(0, -1);
				this.render(this.getTitle(2) + blackString + '\n\n未記錄體溫總人數：' + blackList.length);
				CG.Base.hideCGPreloader();
			}
			catch (err) {
				console.log(err);
				this.render('錯誤' + err);
			}
		})
	}

	private getTitle(cond: number): string {
		let timeState = '晨';
		cond == 2 && (timeState = '晚');
		let year = new Date().getFullYear() - 1911;
		let month = new Date().getMonth() + 1;
		let date = new Date().getDate();
		let day: string | number = new Date().getDay();
		switch (day) {
			case 1:
				day = '一';
				break;
			case 2:
				day = '二';
				break;
			case 3:
				day = '三';
				break;
			case 4:
				day = '四';
				break;
			case 5:
				day = '五';
				break;
			case 6:
				day = '六';
				break;
			case 0:
				day = '日';
		}
		let hour: string | number = new Date().getHours();
		hour < 10 && (hour = '0' + hour);
		let minute: string | number = new Date().getMinutes();
		minute < 10 && (minute = '0' + minute);
		let title = year + '年' + month + '月' + date + '日' + '(' + day + ')\n未依規定時間記錄' + timeState + '間體溫者' + '(' + hour + minute + '前)' + '\n\n學號：'
		return title;
	}

	private render(title: string) {
		let oldClass = document.body.getElementsByClassName('morning');
		oldClass && oldClass.item(0) && oldClass.item(0).remove();
		let blOnScreen = document.createElement('div');
		blOnScreen.className = 'morning'
		blOnScreen.innerText = title;
		blOnScreen.style.cssText = 'position: abolute; top:0; left: 0; z-index: 1000; display: flex; color: white';
		document.body.appendChild(blOnScreen);
	}
}

export const APP = new App();
