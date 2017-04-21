# 许可证（GPLv3）

ArduPilot（包括Copter, Plane, Rover和AntennaTracker）和Mission Planner是免费软件：您可以根据[自由软件基金会](http://www.fsf.org/)发布的GNU通用公共许可证版本3（GPLv3，General Public License version 3 ）的条款重新修改发布它。

这个程序发布的目的是希望帮助到您，但没有任何保障; 甚至没有适销性或适用于特定用途的默认保证。有关详细信息，请参阅GNU通用公共许可证（GPLv3）。

有关更多具体细节，请参阅http://www.gnu.org/licenses， [GPLv3快速指南](www.gnu.org/licenses/quick-guide-gplv3.html)和代码库中的[copying.txt](https://github.com/ArduPilot/ardupilot/blob/master/COPYING.txt)文件。

你可以查看相同许可证的GNU操作系统的[常见问题](www.gnu.org/licenses/gpl-faq.html)。

## 致开发者

我们非常感谢您使用我们的代码来做有意义的事情。 在使用源码时，您可能会发现并修复BUG，或者添加对社区更有用的功能，希望你在源码架构中把你做的修改或遇到的问题记录下来，pull request到主库，以使更多开发者了解。

## 致销售此产品的公司或个人

我们也非常感谢那些把这个软件并入他们的产品出售的公司和个人。 有许多事情需要许可证，但是以下几点我们需要特别指出：

* 通知客户飞行代码是开源的，并在产品中提供实际的源代码，或提供可以找到源代码的链接（参见下面的示例）。
![](http://ardupilot.org/dev/_images/license-sample-web-page.png)

* 与个体开发者的贡献一样，如果您可以通过电子邮件发送给drones-discuss@googlegroups.com，通知我们了解包含该软件的产品，我们将会非常感激。对于那些活跃社区提交给原始代码库有用的更改，我们也会感激。

对于个体开发者和公司，我们还要求，在制作衍生作品时，列出所有对该当前软件做贡献的个人。

## 为什么我们选择这个许可证呢？

* 对项目的bug修复和扩展（或至少提供这些修复给客户）的要求增加了贡献者之间的合作。 没有这个要求，参与者试图对自己进行小的改进，以获得比其他贡献者更多的优势。 有证据表明，这很快就导致了许多不符合项目的难题，造成了所有人的损害。

Linus Torvalds（Linux的发明者）同意这一观点。
![](http://ardupilot.org/dev/_images/license-linus-quote.png)

* 许可证的“v3”部分确保购买飞机的客户有权在飞行控制器上升级或更换ArduPilot软件版本。 许可证不要求它实际工作，只是让升级成为可能。 这确保即使制造商停止支持产品（这种情况时常发生），如果使用者或社区的开发人员决定接受支持，产品仍将继续有用。 这样的例子已经发生在ArduPilot。

## 是否可以集成封闭源（即专有）和开源？

Ardupilot是开放源代码（GPLv3），但您可以使用配套硬件来运行封闭的源代码，将ArduPilot集成到企业系统中，或者添加更高级别的功能来区分您的竞争对手。 您可以利用免费的低级别飞行代码的可靠性来扩展更高级别的功能。 我们相信ArduPilot与领先的封闭系统一样可靠，您无需对特定制造商感到抱歉。 下面是一个制造商案例。
![](http://ardupilot.org/dev/_images/license-integrating-open-and-closed.png)
