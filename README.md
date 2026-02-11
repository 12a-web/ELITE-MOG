# ELITE-MOG
import React, { useState } from "react";
import { motion } from "framer-motion";
import { CheckCircle, ShieldCheck, Star, Lock } from "lucide-react";

/**
 * ELITE MOG — Premium appearance coaching landing page
 * ✅ Modern, legit look
 * ✅ Form collects: name + email + mobile + message
 * ✅ Pay-on-site flow via Stripe Payment Link (Apple Pay supported via Stripe)
 *
 * HOW PAYMENTS WORK (REAL):
 * - This site sends the customer to Stripe Checkout using a Stripe Payment Link.
 * - Apple Pay shows automatically in Stripe Checkout IF you enable it in Stripe + verify your domain,
 *   and if the buyer’s device/browser supports it (ex: iPhone/Safari).
 */

// 1) Paste your real Stripe Payment Link here
// Example looks like: "https://buy.stripe.com/xxxxxx"
const STRIPE_PAYMENT_LINK = "YOUR_STRIPE_PAYMENT_LINK_HERE";

// 2) Hero image: put a good-looking model photo here
// Option A (recommended): save your hero image as /public/elite-mog-hero.jpg and use "/elite-mog-hero.jpg"
// Option B: use any hosted image URL
const HERO_IMAGE_SRC = "/elite-mog-hero.jpg";

export default function EliteMog() {
  const [submitted, setSubmitted] = useState(false);
  const [form, setForm] = useState({
    name: "",
    email: "",
    phone: "",
    goals: "",
    paid: false,
  });

  function updateField(key) {
    return (e) => setForm((p) => ({ ...p, [key]: e.target.value }));
  }

  function updatePaid(e) {
    setForm((p) => ({ ...p, paid: e.target.checked }));
  }

  const canSubmit =
    form.name.trim() &&
    form.email.trim() &&
    form.phone.trim() &&
    form.paid;

  const handleSubmit = (e) => {
    e.preventDefault();
    if (!canSubmit) return;
    setSubmitted(true);
  };

  return (
    <div className="min-h-screen bg-slate-950 text-white">
      {/* NAV */}
      <header className="border-b border-white/10 backdrop-blur sticky top-0 bg-slate-950/80 z-50">
        <div className="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
          <a href="#" className="text-2xl font-extrabold tracking-tight">
            ELITE <span className="text-indigo-400">MOG</span>
          </a>

          <div className="flex items-center gap-3">
            <a
              href="#pricing"
              className="hidden sm:inline-flex rounded-xl px-4 py-2 text-sm font-semibold text-slate-200 hover:bg-white/5 transition"
            >
              Pricing
            </a>
            <a
              href="#signup"
              className="bg-indigo-500 hover:bg-indigo-600 px-5 py-2 rounded-xl font-semibold transition"
            >
              Get Advice
            </a>
          </div>
        </div>
      </header>

      {/* HERO */}
      <section className="max-w-6xl mx-auto px-6 py-16 md:py-20 grid md:grid-cols-2 gap-12 items-center">
        <div>
          <motion.h1
            initial={{ opacity: 0, y: 18 }}
            animate={{ opacity: 1, y: 0 }}
            className="text-4xl md:text-5xl font-extrabold leading-tight tracking-tight"
          >
            Look sharper.
            <span className="block text-indigo-400">Feel more confident.</span>
          </motion.h1>

          <p className="mt-6 text-slate-300 text-lg max-w-prose">
            ELITE MOG is a premium 1-on-1 appearance coaching session focused on
            practical upgrades: grooming, style, haircut choices, skincare
            basics, posture, and a simple plan you can follow.
          </p>

          <div className="mt-8 flex flex-wrap gap-3">
            <a
              href="#signup"
              className="bg-indigo-500 hover:bg-indigo-600 px-6 py-3 rounded-xl font-bold transition"
            >
              Book a Session
            </a>
            <a
              href="#how"
              className="bg-white/5 hover:bg-white/10 px-6 py-3 rounded-xl font-semibold transition"
            >
              How it works
            </a>
          </div>

          <div className="mt-10 flex flex-wrap gap-6 text-sm text-slate-300/90">
            <div className="flex items-center gap-2">
              <ShieldCheck size={18} className="text-indigo-300" />
              Secure Stripe Checkout
            </div>
            <div className="flex items-center gap-2">
              <Star size={18} className="text-indigo-300" />
              Personalized plan
            </div>
            <div className="flex items-center gap-2">
              <Lock size={18} className="text-indigo-300" />
              Private & confidential
            </div>
          </div>

          <div className="mt-4 text-xs text-slate-400">
            Apple Pay is available inside Stripe Checkout when enabled + supported.
          </div>
        </div>

        {/* HERO IMAGE */}
        <div className="relative">
          <div className="absolute -inset-6 bg-indigo-500/20 blur-3xl rounded-3xl" />
          <div className="relative rounded-3xl border border-white/10 overflow-hidden shadow-2xl">
            <img
              src={HERO_IMAGE_SRC}
              alt="Elite Mog hero model"
              className="h-[520px] w-full object-cover"
              onError={(e) => {
                // fallback in case user hasn't added the local image yet
                e.currentTarget.src =
                  "https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&w=1400&q=80";
              }}
            />
            <div className="absolute inset-x-0 bottom-0 p-5 bg-gradient-to-t from-slate-950/90 via-slate-950/35 to-transparent">
              <div className="flex items-center justify-between gap-4">
                <div>
                  <div className="text-sm font-semibold">Premium session</div>
                  <div className="text-xs text-slate-300">
                    Grooming • Style • Confidence • Plan
                  </div>
                </div>
                <div className="rounded-2xl bg-white/10 border border-white/10 px-4 py-2 text-sm font-semibold">
                  $30
                </div>
              </div>
            </div>
          </div>
          <div className="mt-3 text-xs text-slate-500">
            To use your own “tan / colored eyes / clean face” image: save it as{" "}
            <span className="font-semibold text-slate-300">public/elite-mog-hero.jpg</span>.
          </div>
        </div>
      </section>

      {/* TRUST */}
      <section id="how" className="border-t border-white/10">
        <div className="max-w-6xl mx-auto px-6 py-16 grid md:grid-cols-3 gap-10">
          <div className="rounded-3xl bg-white/5 border border-white/10 p-6">
            <h3 className="font-bold text-xl">Personalized Strategy</h3>
            <p className="text-slate-300/90 mt-2">
              Advice tailored to your goals, features, and style preferences.
              No generic copy-paste tips.
            </p>
          </div>

          <div className="rounded-3xl bg-white/5 border border-white/10 p-6">
            <h3 className="font-bold text-xl">Private & Confidential</h3>
            <p className="text-slate-300/90 mt-2">
              Your info stays private. You choose how much you share.
            </p>
          </div>

          <div className="rounded-3xl bg-white/5 border border-white/10 p-6">
            <h3 className="font-bold text-xl">Actionable Plan</h3>
            <p className="text-slate-300/90 mt-2">
              You leave with a simple checklist: what to change this week and
              what to build long-term.
            </p>
          </div>
        </div>
      </section>

      {/* PRICING */}
      <section id="pricing" className="bg-slate-900/40 border-y border-white/10">
        <div className="max-w-4xl mx-auto px-6 py-18 md:py-20 text-center">
          <h2 className="text-4xl font-extrabold">One Flat Price</h2>
          <p className="text-slate-300/90 mt-3">
            Pay once, get a focused session + practical steps you can actually follow.
          </p>

          <div className="mt-10 bg-slate-950/70 rounded-3xl p-10 border border-white/10 shadow-xl">
            <div className="text-6xl font-extrabold">$30</div>
            <div className="text-slate-300/80 mt-2">Per Session</div>

            <ul className="mt-8 space-y-3 text-slate-200 text-left max-w-md mx-auto">
              <li>✔ Grooming & haircut direction</li>
              <li>✔ Skin basics + routine suggestions</li>
              <li>✔ Style upgrades (fits, colors, basics)</li>
              <li>✔ Confidence / posture tips</li>
              <li>✔ Clear next steps</li>
            </ul>

            <a
              href="#signup"
              className="inline-block mt-8 bg-indigo-500 hover:bg-indigo-600 px-8 py-3 rounded-xl font-bold transition"
            >
              Book Your Session
            </a>

            <div className="mt-4 text-xs text-slate-400">
              Payments are processed securely by Stripe. Apple Pay appears on supported devices when enabled.
            </div>
          </div>
        </div>
      </section>

      {/* SIGNUP FORM */}
      <section id="signup" className="max-w-3xl mx-auto px-6 py-18 md:py-20">
        <h2 className="text-4xl font-extrabold text-center">Apply for ELITE MOG</h2>
        <p className="text-slate-300/90 text-center mt-3">
          Fill this out and complete payment to lock your session.
          <span className="block mt-2 text-xs text-slate-400">
            Apple Pay will show on the Stripe Checkout page if enabled + supported.
          </span>
        </p>

        {!submitted ? (
          <form
            onSubmit={handleSubmit}
            className="mt-10 bg-slate-950/70 p-8 md:p-10 rounded-3xl border border-white/10 space-y-5 shadow-xl"
          >
            <div className="grid md:grid-cols-2 gap-4">
              <input
                required
                value={form.name}
                onChange={updateField("name")}
                placeholder="Full Name"
                className="w-full p-4 rounded-xl bg-slate-950 border border-white/10 focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />

              <input
                required
                type="email"
                value={form.email}
                onChange={updateField("email")}
                placeholder="Email Address"
                className="w-full p-4 rounded-xl bg-slate-950 border border-white/10 focus:outline-none focus:ring-2 focus:ring-indigo-500"
              />
            </div>

            <input
              required
              type="tel"
              inputMode="tel"
              value={form.phone}
              onChange={updateField("phone")}
              placeholder="Mobile Phone Number"
              className="w-full p-4 rounded-xl bg-slate-950 border border-white/10 focus:outline-none focus:ring-2 focus:ring-indigo-500"
            />

            <textarea
              value={form.goals}
              onChange={updateField("goals")}
              placeholder="What do you want to improve? (grooming, hair, style, skincare, confidence, etc.)"
              className="w-full p-4 rounded-xl bg-slate-950 border border-white/10 focus:outline-none focus:ring-2 focus:ring-indigo-500"
              rows={4}
            />

            <div className="rounded-2xl bg-white/5 border border-white/10 p-4 text-sm text-slate-200">
              <div className="font-semibold">Payment</div>
              <div className="mt-1 text-slate-300/80">
                Click the button below to pay $30 via secure Stripe Checkout.
                Apple Pay may appear on supported devices.
              </div>
            </div>

            <a
              href={STRIPE_PAYMENT_LINK}
              target="_blank"
              rel="noreferrer"
              className="block text-center bg-indigo-500 hover:bg-indigo-600 p-4 rounded-xl font-bold transition"
            >
              Pay $30 (Apple Pay / Card)
            </a>

            <label className="flex items-center gap-3 text-sm text-slate-200">
              <input
                type="checkbox"
                checked={form.paid}
                onChange={updatePaid}
                className="h-4 w-4 rounded"
                required
              />
              I completed payment (required)
            </label>

            <button
              type="submit"
              disabled={!canSubmit}
              className={`w-full font-bold p-4 rounded-xl transition ${
                canSubmit
                  ? "bg-white text-black hover:bg-slate-200"
                  : "bg-white/20 text-white/60 cursor-not-allowed"
              }`}
            >
              Submit Application
            </button>

            <div className="text-xs text-slate-400">
              After you submit, you’ll see confirmation here. You’ll be contacted using your email/phone.
            </div>
          </form>
        ) : (
          <div className="mt-10 text-center bg-slate-950/70 p-10 rounded-3xl border border-white/10 shadow-xl">
            <CheckCircle size={54} className="mx-auto text-green-400" />
            <h3 className="text-2xl font-bold mt-4">Application Received</h3>
            <p className="text-slate-300/90 mt-2">
              If payment was completed, you’ll be contacted shortly to schedule your session.
            </p>
            <a
              href="#"
              onClick={() => setSubmitted(false)}
              className="inline-block mt-6 text-indigo-300 hover:text-indigo-200 font-semibold"
            >
              Submit another
            </a>
          </div>
        )}
      </section>

      {/* FOOTER */}
      <footer className="border-t border-white/10 py-10 text-center text-slate-500 text-sm">
        © {new Date().getFullYear()} ELITE MOG. All rights reserved.
      </footer>
    </div>
  );
}
