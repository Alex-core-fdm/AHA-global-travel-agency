# 🌍 AHA Global Travel Agency

✨ **Special 3-Night Singapore Tours** (for ages 60–80, anniversary couples)

---

### 松 (Pine) Package
Gentle Discovery – Comfort-first exploration  
💰 Price: ¥158,000

### 竹 (Bamboo) Package
Balanced Adventure – Comfort + exploration  
💰 Price: ¥178,000

### 海 (Ocean) Package
Elegant Escape – Premium experience, anniversary perks  
💰 Price: ¥218,000

import * as React from "react";
import { Plane, MapPin, Calendar, Users, Heart, ShieldCheck, Clock, Sparkles, Star, Menu, Sun, Moon } from "lucide-react";
import { Button } from "@/components/ui/button";
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Textarea } from "@/components/ui/textarea";
import { Label } from "@/components/ui/label";
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription, DialogTrigger } from "@/components/ui/dialog";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import { Accordion, AccordionItem, AccordionTrigger, AccordionContent } from "@/components/ui/accordion";

// AHA Global Travel Agency — Single-file React page (TSX)
// - TailwindCSS for styling
// - shadcn/ui components
// - Lucide icons
// Drop into your project as src/pages/AhaLanding.tsx (or similar) and route to it.

// Dark mode toggle
function DarkModeToggle() {
  const [enabled, setEnabled] = React.useState<boolean>(() => {
    if (typeof document === "undefined") return false;
    return document.documentElement.classList.contains("dark");
  });
  React.useEffect(() => {
    if (typeof document === "undefined") return;
    document.documentElement.classList.toggle("dark", enabled);
  }, [enabled]);
  return (
    <button
      aria-label="Toggle dark mode"
      onClick={() => setEnabled((v) => !v)}
      className="inline-flex items-center gap-2 rounded-full border px-3 py-1.5 text-sm hover:bg-muted"
    >
      {enabled ? <Sun className="h-4 w-4" /> : <Moon className="h-4 w-4" />}
      <span className="hidden sm:inline">{enabled ? "Light" : "Dark"} mode</span>
    </button>
  );
}

// Simple nav link component
function NavLink({ children, href }: { children: React.ReactNode; href: string }) {
  return (
    <a href={href} className="text-sm font-medium text-muted-foreground hover:text-foreground">
      {children}
    </a>
  );
}

// Tour card
type Tour = {
  id: string;
  tier: "松" | "竹" | "海";
  name: string;
  description: string;
  price: string;
  nights: number;
  location: string;
  perks: string[];
  image: string;
  seniorFriendly?: boolean;
  anniversaryPerk?: boolean;
};

const tours: Tour[] = [
  {
    id: "pine",
    tier: "松",
    name: "Pine — Gentle Discovery",
    description:
      "Unhurried pacing, accessible routes, and curated highlights. Ideal for seniors seeking comfort-first exploration.",
    price: "¥158,000",
    nights: 3,
    location: "Singapore",
    perks: ["Express coach for city touring", "Local guide arranged via hotel", "Daily breakfast & dinner", "Health check support"],
    image:
      "https://images.unsplash.com/photo-1525625293386-3f8f99389edd?q=80&w=2070&auto=format&fit=crop",
    seniorFriendly: true,
    anniversaryPerk: true,
  },
  {
    id: "bamboo",
    tier: "竹",
    name: "Bamboo — Balanced Adventure",
    description:
      "A comfortable rhythm with a touch more exploration—gardens, museums, and night safaris at a steady pace.",
    price: "¥178,000",
    nights: 3,
    location: "Singapore",
    perks: ["Hotel-arranged guide", "Breakfast & dinner included", "Priority bus seating", "Flexible afternoon breaks"],
    image:
      "https://images.unsplash.com/photo-1512453979798-5ea266f8880c?q=80&w=2070&auto=format&fit=crop",
    seniorFriendly: true,
    anniversaryPerk: true,
  },
  {
    id: "ocean",
    tier: "海",
    name: "Ocean — Elegant Escape",
    description:
      "Premium hotels, concierge care, and exclusive experiences for couples celebrating milestones.",
    price: "¥218,000",
    nights: 3,
    location: "Singapore",
    perks: ["Anniversary dinner upgrade", "Airport concierge", "Spa time block", "Sunset river cruise"],
    image:
      "https://images.unsplash.com/photo-1506806732259-39c2d0268443?q=80&w=2070&auto=format&fit=crop",
    seniorFriendly: true,
    anniversaryPerk: true,
  },
];

// Destination gallery
const destinations = [
  { name: "Singapore", image: "https://images.unsplash.com/photo-1525625293386-3f8f99389edd?q=80&w=1600&auto=format&fit=crop" },
  { name: "Kyoto", image: "https://images.unsplash.com/photo-1550136513-548af4445339?q=80&w=1600&auto=format&fit=crop" },
  { name: "Bangkok", image: "https://images.unsplash.com/photo-1508002366005-75a695ee2ab0?q=80&w=1600&auto=format&fit=crop" },
  { name: "Bali", image: "https://images.unsplash.com/photo-1537996194471-e657df975ab4?q=80&w=1600&auto=format&fit=crop" },
  { name: "Seoul", image: "https://images.unsplash.com/photo-1549692520-acc6669e2f0c?q=80&w=1600&auto=format&fit=crop" },
  { name: "Taipei", image: "https://images.unsplash.com/photo-1577493340887-b7bfff550145?q=80&w=1600&auto=format&fit=crop" },
];

function Stat({ value, label }: { value: string; label: string }) {
  return (
    <div className="rounded-2xl border bg-background/60 px-6 py-4 text-center shadow-sm backdrop-blur">
      <div className="text-2xl font-semibold tracking-tight">{value}</div>
      <div className="text-xs text-muted-foreground">{label}</div>
    </div>
  );
}

function ValueCard({ icon, title, desc }: { icon: React.ReactNode; title: string; desc: string }) {
  return (
    <Card className="h-full border-muted/50">
      <CardHeader className="space-y-1">
        <div className="flex items-center gap-3">
          <div className="rounded-xl border p-2">{icon}</div>
          <CardTitle className="text-base">{title}</CardTitle>
        </div>
        <CardDescription className="text-sm leading-relaxed">{desc}</CardDescription>
      </CardHeader>
    </Card>
  );
}

function TourCard({ tour }: { tour: Tour }) {
  return (
    <Card className="overflow-hidden border-muted/50">
      <div className="relative h-52 w-full overflow-hidden">
        {/* eslint-disable-next-line @next/next/no-img-element */}
        <img src={tour.image} alt={`${tour.name} photo`} className="h-full w-full object-cover transition-transform duration-500 hover:scale-105" />
        <div className="absolute left-3 top-3 rounded-full bg-background/80 px-3 py-1 text-xs shadow-sm backdrop-blur">
          {tour.tier}・{tour.location}
        </div>
      </div>
      <CardHeader>
        <div className="flex items-start justify-between gap-4">
          <div>
            <CardTitle className="text-lg">{tour.name}</CardTitle>
            <CardDescription>{tour.description}</CardDescription>
          </div>
          <div className="text-right">
            <div className="text-lg font-semibold">{tour.price}</div>
            <div className="text-xs text-muted-foreground">{tour.nights} nights</div>
          </div>
        </div>
      </CardHeader>
      <CardContent className="grid gap-3">
        <ul className="grid grid-cols-1 gap-2 text-sm sm:grid-cols-2">
          {tour.perks.map((p) => (
            <li key={p} className="flex items-center gap-2 text-muted-foreground">
              <ShieldCheck className="h-4 w-4" /> {p}
            </li>
          ))}
        </ul>
        <div className="flex items-center justify-between pt-2">
          <div className="flex items-center gap-2 text-xs text-muted-foreground">
            {tour.seniorFriendly && (
              <span className="inline-flex items-center gap-1 rounded-full border px-2 py-1"><Heart className="h-3 w-3" /> Senior-friendly</span>
            )}
            {tour.anniversaryPerk && (
              <span className="inline-flex items-center gap-1 rounded-full border px-2 py-1"><Sparkles className="h-3 w-3" /> 20-year anniversary gift</span>
            )}
          </div>
          <Dialog>
            <DialogTrigger asChild>
              <Button size="sm">Book inquiry</Button>
            </DialogTrigger>
            <DialogContent className="sm:max-w-lg">
              <DialogHeader>
                <DialogTitle>Inquiry — {tour.name}</DialogTitle>
                <DialogDescription>Tell us a bit about your trip and we'll reply with options and pricing details.</DialogDescription>
              </DialogHeader>
              <form className="grid gap-4">
                <div className="grid gap-2">
                  <Label htmlFor="name">Full name</Label>
                  <Input id="name" placeholder="Your name" />
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="email">Email</Label>
                  <Input id="email" type="email" placeholder="you@example.com" />
                </div>
                <div className="grid gap-2 sm:grid-cols-3">
                  <div className="grid gap-2">
                    <Label htmlFor="dates">Dates</Label>
                    <Input id="dates" placeholder="2025-10-12 → 2025-10-15" />
                  </div>
                  <div className="grid gap-2">
                    <Label htmlFor="guests">Guests</Label>
                    <Input id="guests" type="number" placeholder="2" />
                  </div>
                  <div className="grid gap-2">
                    <Label htmlFor="tier">Tier</Label>
                    <Input id="tier" defaultValue={`${tour.tier}`} />
                  </div>
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="message">Notes</Label>
                  <Textarea id="message" placeholder="Mobility needs, dietary preferences, anniversary date, etc." />
                </div>
                <Button type="button">Send inquiry</Button>
              </form>
            </DialogContent>
          </Dialog>
        </div>
      </CardContent>
    </Card>
  );
}

function Header() {
  const [open, setOpen] = React.useState(false);
  return (
    <header className="sticky top-0 z-40 w-full border-b bg-background/80 backdrop-blur">
      <div className="mx-auto flex max-w-7xl items-center justify-between px-4 py-3 sm:px-6">
        <a href="#home" className="flex items-center gap-2">
          <div className="flex h-9 w-9 items-center justify-center rounded-xl border text-primary">
            <Plane className="h-5 w-5" />
          </div>
          <div className="leading-tight">
            <div className="text-sm font-semibold tracking-wide">AHA Global</div>
            <div className="text-[10px] text-muted-foreground">Travel Agency</div>
          </div>
        </a>
        <nav className="hidden items-center gap-6 md:flex">
          <NavLink href="#tours">Tours</NavLink>
          <NavLink href="#destinations">Destinations</NavLink>
          <NavLink href="#why">Why AHA</NavLink>
          <NavLink href="#faq">FAQ</NavLink>
          <a href="https://www.AHAglobaltravelagency.com" className="text-sm text-primary underline-offset-4 hover:underline">AHAglobaltravelagency.com</a>
        </nav>
        <div className="flex items-center gap-3">
          <DarkModeToggle />
          <Button className="hidden sm:inline-flex" size="sm">Contact us</Button>
          <button className="md:hidden" onClick={() => setOpen((v) => !v)} aria-label="Open menu">
            <Menu className="h-5 w-5" />
          </button>
        </div>
      </div>
      {open && (
        <div className="border-t bg-background md:hidden">
          <div className="mx-auto grid max-w-7xl gap-2 px-4 py-3 sm:px-6">
            <NavLink href="#tours">Tours</NavLink>
            <NavLink href="#destinations">Destinations</NavLink>
            <NavLink href="#why">Why AHA</NavLink>
            <NavLink href="#faq">FAQ</NavLink>
            <Button size="sm" className="mt-2 w-fit">Contact us</Button>
          </div>
        </div>
      )}
    </header>
  );
}

function Hero() {
  return (
    <section id="home" className="relative overflow-hidden">
      <div className="absolute inset-0 -z-10 bg-gradient-to-b from-primary/10 via-transparent to-transparent" />
      <div className="mx-auto grid max-w-7xl items-center gap-8 px-4 pb-16 pt-14 sm:px-6 md:grid-cols-2 md:pb-24 md:pt-20">
        <div className="space-y-6">
          <div className="inline-flex items-center gap-2 rounded-full border px-3 py-1 text-xs text-muted-foreground">
            <ShieldCheck className="h-3.5 w-3.5" /> Senior‑friendly curated tours
          </div>
          <h1 className="text-3xl font-semibold leading-tight sm:text-4xl md:text-5xl">
            AHA Global Travel Agency
          </h1>
          <p className="max-w-prose text-muted-foreground">
            Thoughtfully designed journeys with comfort, safety, and celebration in mind. Ideal for travelers aged 60–80 and couples commemorating their 20‑year anniversary.
          </p>
          <div className="grid gap-3 rounded-2xl border bg-background/60 p-3 shadow-sm backdrop-blur sm:grid-cols-4">
            <div className="col-span-2 grid gap-1">
              <Label htmlFor="where" className="text-xs">Where</Label>
              <div className="flex items-center gap-2">
                <MapPin className="h-4 w-4 text-muted-foreground" />
                <Input id="where" placeholder="Singapore" className="bg-background" />
              </div>
            </div>
            <div className="grid gap-1">
              <Label htmlFor="dates" className="text-xs">Dates</Label>
              <div className="flex items-center gap-2">
                <Calendar className="h-4 w-4 text-muted-foreground" />
                <Input id="dates" placeholder="2025/10/12 → 10/15" className="bg-background" />
              </div>
            </div>
            <div className="grid gap-1">
              <Label htmlFor="guests" className="text-xs">Guests</Label>
              <div className="flex items-center gap-2">
                <Users className="h-4 w-4 text-muted-foreground" />
                <Input id="guests" placeholder="20" className="bg-background" />
              </div>
            </div>
            <div className="sm:col-span-4">
              <Button className="w-full">Search availability</Button>
            </div>
          </div>
          <div className="flex gap-4">
            <Stat value="4.9/5" label="Guest rating" />
            <Stat value="12k+" label="Happy travelers" />
            <Stat value="98%" label="On‑time tours" />
          </div>
        </div>
        {/* eslint-disable-next-line @next/next/no-img-element */}
        <img
          src="https://images.unsplash.com/photo-1544989164-31dc3c645987?q=80&w=2070&auto=format&fit=crop"
          alt="Travel collage"
          className="h-[420px] w-full rounded-3xl object-cover shadow-xl"
        />
      </div>
    </section>
  );
}

function WhyAHA() {
  return (
    <section id="why" className="mx-auto max-w-7xl px-4 py-16 sm:px-6">
      <div className="mx-auto max-w-2xl text-center">
        <h2 className="text-2xl font-semibold sm:text-3xl">Why travel with AHA?</h2>
        <p className="mt-2 text-muted-foreground">Comfort-first design, clear pacing, and thoughtful care—without compromising on wonder.</p>
      </div>
      <div className="mt-8 grid gap-4 sm:grid-cols-2 md:grid-cols-4">
        <ValueCard icon={<Clock className="h-5 w-5" />} title="Gentle pacing" desc="Itineraries tuned for energy and rest, including afternoon breaks." />
        <ValueCard icon={<ShieldCheck className="h-5 w-5" />} title="Safety & support" desc="Local guides via hotel partners, health check assistance, and reliable transport." />
        <ValueCard icon={<Heart className="h-5 w-5" />} title="Anniversary perks" desc="Special upgrades for couples celebrating 20 years together." />
        <ValueCard icon={<Sparkles className="h-5 w-5" />} title="Curated moments" desc="Meaningful highlights and photo‑ready scenes—no rush, just joy." />
      </div>
    </section>
  );
}

function FeaturedTours() {
  return (
    <section id="tours" className="mx-auto max-w-7xl px-4 py-16 sm:px-6">
      <div className="flex items-end justify-between gap-4">
        <div>
          <h2 className="text-2xl font-semibold sm:text-3xl">Featured 3‑Night Singapore</h2>
          <p className="text-muted-foreground">Choose your style: 松 (Pine), 竹 (Bamboo), or 海 (Ocean).</p>
        </div>
        <Tabs defaultValue="all" className="hidden sm:block">
          <TabsList>
            <TabsTrigger value="all">All</TabsTrigger>
            <TabsTrigger value="senior">Senior‑friendly</TabsTrigger>
            <TabsTrigger value="anniversary">Anniversary</TabsTrigger>
          </TabsList>
        </Tabs>
      </div>
      <div className="mt-6 grid gap-6 md:grid-cols-2 lg:grid-cols-3">
        {tours.map((t) => (
          <TourCard key={t.id} tour={t} />
        ))}
      </div>
      <div className="mt-8 rounded-2xl border bg-primary/5 p-6 text-center">
        <div className="mx-auto max-w-3xl">
          <p className="text-sm text-primary">Limited‑time offer</p>
          <h3 className="mt-2 text-xl font-semibold">Special promotion for couples celebrating their 20‑year anniversary (ages 60–80)</h3>
          <p className="mt-2 text-muted-foreground">
            Enjoy a complimentary anniversary dinner experience and priority coach seating for two on any 松・竹・海 package.
          </p>
          <Button className="mt-4">Claim anniversary perk</Button>
        </div>
      </div>
    </section>
  );
}

function Destinations() {
  return (
    <section id="destinations" className="mx-auto max-w-7xl px-4 py-16 sm:px-6">
      <div className="mx-auto max-w-2xl text-center">
        <h2 className="text-2xl font-semibold sm:text-3xl">Explore destinations</h2>
        <p className="mt-2 text-muted-foreground">Handpicked cities with excellent accessibility, cuisine, and culture.</p>
      </div>
      <div className="mt-8 grid gap-4 sm:grid-cols-2 md:grid-cols-3">
        {destinations.map((d) => (
          <div key={d.name} className="group relative overflow-hidden rounded-2xl border">
            {/* eslint-disable-next-line @next/next/no-img-element */}
            <img src={d.image} alt={d.name} className="h-52 w-full object-cover transition-transform duration-500 group-hover:scale-105" />
            <div className="pointer-events-none absolute inset-0 bg-gradient-to-t from-black/60 via-black/0 to-black/0" />
            <div className="absolute bottom-3 left-3 flex items-center gap-2 text-white">
              <MapPin className="h-4 w-4" /> <span className="text-sm font-medium">{d.name}</span>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function Testimonials() {
  return (
    <section className="mx-auto max-w-7xl px-4 py-16 sm:px-6">
      <div className="mx-auto max-w-2xl text-center">
        <h2 className="text-2xl font-semibold sm:text-3xl">Guest stories</h2>
        <p className="mt-2 text-muted-foreground">Real words from travelers who trusted AHA with their special moments.</p>
      </div>
      <div className="mt-8 grid gap-6 md:grid-cols-3">
        {[0, 1, 2].map((i) => (
          <Card key={i} className="border-muted/50">
            <CardHeader>
              <div className="flex items-center justify-between">
                <CardTitle className="text-base">Wonderful pacing & care</CardTitle>
                <div className="flex items-center gap-1 text-yellow-500" aria-label="5 stars">
                  <Star className="h-4 w-4 fill-current" />
                  <Star className="h-4 w-4 fill-current" />
                  <Star className="h-4 w-4 fill-current" />
                  <Star className="h-4 w-4 fill-current" />
                  <Star className="h-4 w-4 fill-current" />
                </div>
              </div>
              <CardDescription>
                “We celebrated our 20‑year anniversary in Singapore. The coach, guides, and gentle schedule made it perfect.”
              </CardDescription>
            </CardHeader>
            <CardContent>
              <div className="text-xs text-muted-foreground">— Mr. & Mrs. Tanaka</div>
            </CardContent>
          </Card>
        ))}
      </div>
    </section>
  );
}

function FAQ() {
  return (
    <section id="faq" className="mx-auto max-w-4xl px-4 py-16 sm:px-6">
      <div className="text-center">
        <h2 className="text-2xl font-semibold sm:text-3xl">Frequently asked questions</h2>
      </div>
      <Accordion type="single" collapsible className="mt-6">
        <AccordionItem value="item-1">
          <AccordionTrigger className="text-left">Is this suitable for travelers aged 60–80?</AccordionTrigger>
          <AccordionContent>
            Absolutely. All AHA itineraries are designed with comfortable pacing, accessible routes, and health‑check support.
          </AccordionContent>
        </AccordionItem>
        <AccordionItem value="item-2">
          <AccordionTrigger className="text-left">What’s included in the 3‑night Singapore tour?</AccordionTrigger>
          <AccordionContent>
            Daily breakfast and dinner, express coach for city touring, hotel‑arranged local guide, and optional upgrades for anniversaries.
          </AccordionContent>
        </AccordionItem>
        <AccordionItem value="item-3">
          <AccordionTrigger className="text-left">Do you arrange travel & health insurance?</AccordionTrigger>
          <AccordionContent>
            Yes. We can provide quotes for airfare, travel insurance, and senior‑friendly health coverage upon request.
          </AccordionContent>
        </AccordionItem>
      </Accordion>
    </section>
  );
}

function Footer() {
  return (
    <footer className="border-t">
      <div className="mx-auto grid max-w-7xl gap-8 px-4 py-10 sm:grid-cols-2 sm:px-6 md:grid-cols-4">
        <div className="space-y-2">
          <div className="flex items-center gap-2">
            <div className="flex h-8 w-8 items-center justify-center rounded-lg border text-primary">
              <Plane className="h-4 w-4" />
            </div>
            <span className="text-sm font-semibold">AHA Global Travel Agency</span>
          </div>
          <p className="text-sm text-muted-foreground">Comfort‑first journeys for seniors and milestone couples.</p>
        </div>
        <div>
          <div className="text-sm font-semibold">Contact</div>
          <ul className="mt-2 space-y-1 text-sm text-muted-foreground">
            <li>Email: hello@AHAglobaltravelagency.com</li>
            <li>Phone: +81‑00‑0000‑0000</li>
            <li>Address: Osaka, Japan</li>
          </ul>
        </div>
        <div>
          <div className="text-sm font-semibold">Company</div>
          <ul className="mt-2 space-y-1 text-sm text-muted-foreground">
            <li><a href="#tours" className="hover:text-foreground">Tours</a></li>
            <li><a href="#destinations" className="hover:text-foreground">Destinations</a></li>
            <li><a href="#why" className="hover:text-foreground">Why AHA</a></li>
            <li><a href="#faq" className="hover:text-foreground">FAQ</a></li>
          </ul>
        </div>
        <div>
          <div className="text-sm font-semibold">Legal</div>
          <ul className="mt-2 space-y-1 text-sm text-muted-foreground">
            <li>Terms & Conditions</li>
            <li>Privacy Policy</li>
            <li>Insurance Partner Disclosures</li>
          </ul>
        </div>
      </div>
      <div className="border-t py-6 text-center text-xs text-muted-foreground">
        © {new Date().getFullYear()} AHA Global Travel Agency — All rights reserved.
      </div>
    </footer>
  );
}

export default function AhaLanding() {
  return (
    <div className="min-h-screen bg-background text-foreground">
      <Header />
      <Hero />
      <WhyAHA />
      <FeaturedTours />
      <Destinations />
      <Testimonials />
      <FAQ />
      <section className="mx-auto max-w-7xl px-4 pb-20 sm:px-6">
        <div className="rounded-3xl border bg-primary/5 p-8 text-center md:p-12">
          <h3 className="text-xl font-semibold sm:text-2xl">Ready to design your perfect trip?</h3>
          <p className="mt-2 text-muted-foreground">Tell us your dates, group size, and needs—we’ll craft the plan and pricing.</p>
          <Dialog>
            <DialogTrigger asChild>
              <Button className="mt-4">Start a custom plan</Button>
            </DialogTrigger>
            <DialogContent className="sm:max-w-lg">
              <DialogHeader>
                <DialogTitle>Start a custom plan</DialogTitle>
                <DialogDescription>We’ll reply with a tailored itinerary and quote.</DialogDescription>
              </DialogHeader>
              <form className="grid gap-4">
                <div className="grid gap-2">
                  <Label htmlFor="cname">Full name</Label>
                  <Input id="cname" placeholder="Your name" />
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="cemail">Email</Label>
                  <Input id="cemail" type="email" placeholder="you@example.com" />
                </div>
                <div className="grid gap-2 sm:grid-cols-3">
                  <div className="grid gap-2">
                    <Label htmlFor="cdates">Dates</Label>
                    <Input id="cdates" placeholder="2025/10/12 → 10/15" />
                  </div>
                  <div className="grid gap-2">
                    <Label htmlFor="cguests">Guests</Label>
                    <Input id="cguests" type="number" placeholder="20" />
                  </div>
                  <div className="grid gap-2">
                    <Label htmlFor="cdestination">Destination</Label>
                    <Input id="cdestination" placeholder="Singapore" />
                  </div>
                </div>
                <div className="grid gap-2">
                  <Label htmlFor="cnotes">Notes</Label>
                  <Textarea id="cnotes" placeholder="Mobility needs, dietary requests, celebration details, etc." />
                </div>
                <Button type="button">Send request</Button>
              </form>
            </DialogContent>
          </Dialog>
        </div>
      </section>
      <Footer />
    </div>
  );
}

